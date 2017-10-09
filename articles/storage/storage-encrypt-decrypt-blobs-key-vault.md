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
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Tutorial: Encriptar e desencriptar blobs no armazenamento do Microsoft Azure com o Cofre de chaves do Azure
## <a name="introduction"></a>Introdução
Este tutorial abrange como utilizar o toomake de encriptação de armazenamento do lado do cliente com o Cofre de chaves do Azure. Explica como tooencrypt e desencriptar um blob numa aplicação de consola utilização destas tecnologias.

**Estimado tempo toocomplete:** 20 minutos

Para obter informações gerais sobre o Cofre de chaves do Azure, consulte [que é o Cofre de chaves do Azure?](../key-vault/key-vault-whatis.md).

Para obter informações gerais sobre a encriptação do lado do cliente para o Storage do Azure, consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, tem de ter Olá seguintes:

* Uma conta de armazenamento do Azure
* Visual Studio 2013 ou posterior
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Descrição geral de encriptação do lado do cliente
Para obter uma descrição geral de encriptação do lado do cliente para o Storage do Azure, consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](storage-client-side-encryption.md)

Eis uma breve descrição como funciona a encriptação do lado do cliente:

1. SDK do cliente de armazenamento do Azure Olá gera uma chave de encriptação de conteúdo (CEK), que é uma chave simétrica one time utilização.
2. Dados de cliente são encriptados utilizando este CEK.
3. Olá CEK, em seguida, da aplicação (encriptadas) utilizando a chave de encriptação de chaves Olá (de chaves KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e pode ser gerido localmente ou armazenado no Cofre de chaves do Azure. cliente de armazenamento de Olá próprio nunca tem acesso toohello KEK. Apenas ele invoca o algoritmo de chave de moldagem de Olá fornecida pelo Cofre de chaves. Os clientes podem optar toouse fornecedores personalizados para a chave de encapsulamento de aplicações/abertura se pretenderem.
4. Olá dados encriptados em seguida, são carregado toohello serviço de armazenamento do Azure.

## <a name="set-up-your-azure-key-vault"></a>Configurar o seu Cofre de chaves do Azure
Ordem tooproceed com este tutorial, terá de Olá toodo os seguintes passos, que são descritos no tutorial Olá [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md):

* Crie um cofre de chaves.
* Adicione uma chave ou segredo toohello Cofre de chaves.
* Registe uma aplicação no Azure Active Directory.
* Autorize Olá aplicação toouse Olá chave ou segredo.

Certifique-nota do Olá ClientID e ClientSecret que foram gerados ao registar uma aplicação no Azure Active Directory.

Crie ambas as chaves no Cofre de chaves Olá. Partimos do princípio de rest de Olá tutorial Olá que utiliza os seguintes nomes de Olá: ContosoKeyVault e TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Criar uma aplicação de consola com pacotes e AppSettings
No Visual Studio, crie uma nova aplicação de consola.

Adicione pacotes nuget necessário Olá consola do Gestor de pacotes.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Adicione AppSettings toohello App. config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Adicione Olá seguinte `using` instruções e disponibilizar se tooadd um projeto de toohello tooSystem.Configuration referência.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Adicione um método tooget uma aplicação de consola token tooyour
Olá seguinte método é utilizado pelas classes do Cofre de chaves que necessitam de tooauthenticate para o Cofre de chaves de tooyour de acesso.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Armazenamento de acesso e o Cofre de chaves no seu programa
Olá função principal, adicione Olá seguinte código.

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
> Modelos de objetos do Cofre de chaves
> 
> É importante toounderstand que existem objetos de Cofre de chaves, na verdade, dois modelos toobe em consideração: um baseia-se no Olá API de REST (espaço de nomes do KeyVault) e outro Olá é uma extensão para a encriptação do lado do cliente.
> 
> Olá chave de cofre cliente interage com Olá REST API e compreende JSON Web chaves e segredos para dois tipos de Olá das ações que estão incluídas no Cofre de chaves.
> 
> as extensões do Cofre de chave Olá são as classes que parecem criadas especificamente para a encriptação do lado do cliente no armazenamento do Azure. Contêm uma interface de chaves (IKey) e classes com base no conceito Olá de uma resolução de chave. Existem duas implementações do IKey terá tooknow: RSAKey e SymmetricKey. Agora acontecer toocoincide com coisas Olá que estão incluídas no Cofre de chaves, mas neste momento estão classes independentes (para que Olá chave e o segredo obtido ao hello do cliente do Cofre de chave não implementam IKey).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Encriptar blob e carregue
Adicione o seguinte Olá code tooencrypt um blob e carregue-o tooyour conta de armazenamento Azure. Olá **ResolveKeyAsync** método que é utilizado devolve um IKey.

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

Segue-se uma captura de ecrã do Olá [Portal clássico do Azure](https://manage.windowsazure.com) para um blob que foram encriptado através de encriptação do lado do cliente com uma chave armazenada num cofre de chaves. Olá **KeyId** propriedade é Olá URI para a chave de Olá no Cofre de chaves que age como Olá KEK. Olá **EncryptedKey** propriedade contém a versão encriptada Olá de Olá CEK.

![Captura de ecrã que mostra os metadados do Blob que inclui os metadados de encriptação](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Se observar o construtor de BlobEncryptionPolicy Olá, verá que possa aceitar uma chave de e/ou de uma resolução. Tenha em atenção que agora não é possível utilizar uma resolução para a encriptação porque faz atualmente não suportam uma chave de predefinição.
> 
> 

## <a name="decrypt-blob-and-download"></a>Desencriptar BLOBs e transferir
Desencriptação é realmente o utilizador quando utilizar Olá resolução classes fazem sentido. Olá ID da chave de Olá utilizada para encriptação associado blob Olá nos respetivos metadados, pelo que não existe nenhuma razão para a tooretrieve Olá chave e lembre-se a associação de Olá entre chave e BLOBs. Basta ter toomake se que essa chave Olá permanece no Cofre de chaves.   

chave privada do Olá de permaneça uma chave RSA no Cofre de chaves, por isso, para desencriptação toooccur, Olá chave encriptados da Olá metadados do blob que contém Olá CEK é enviado tooKey cofre para a desencriptação.

Adicione Olá seguir o blob de Olá toodecrypt que acabou de carregar.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Existem alguns dos outros tipos de gestão de chaves resoluções toomake mais fácil, incluindo: AggregateKeyResolver e CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Utilize os segredos do Cofre de chaves
Olá forma toouse um segredo com a encriptação do lado do cliente é através de Olá SymmetricKey classe porque um segredo é, essencialmente, uma chave simétrica. No entanto, conforme indicado acima, um segredo no Cofre de chaves não está mapeado exatamente tooa SymmetricKey. Existem alguns aspetos toounderstand:

* chave de Olá num SymmetricKey tem toobe um comprimento fixo: 128, 192, 256, 384 ou 512 bits.
* chave de Olá num SymmetricKey deve ser codificado em Base64.
* Um segredo do Cofre de chaves que será utilizado como um SymmetricKey tem toohave um tipo de conteúdo de "application/octet-stream" no Cofre de chaves.

Eis um exemplo do PowerShell de criar um segredo no Cofre de chaves que podem ser utilizados como uma SymmetricKey.
Tenha em atenção que valor Olá rígido codificada, $key, destina-se apenas a fins de demonstração. No seu próprio código deverá toogenerate esta chave.

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

Na sua aplicação de consola, pode utilizar Olá mesmo chamar como antes tooretrieve neste secreto como um SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
E já está. Divirta-se!

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre como utilizar o armazenamento do Microsoft Azure com c#, consulte [biblioteca do cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Para obter mais informações sobre Olá API de REST do Blob, consulte [API de REST do serviço Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Para informações mais recentes de Olá no armazenamento do Microsoft Azure, visite toohello [blogue de equipa de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
