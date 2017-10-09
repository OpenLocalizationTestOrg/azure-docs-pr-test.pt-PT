---
title: aaaHow toouse Blob storage do Azure do iOS | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="90fc5-103">Como toouse Blob storage do iOS</span><span class="sxs-lookup"><span data-stu-id="90fc5-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="90fc5-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="90fc5-104">Overview</span></span>
<span data-ttu-id="90fc5-105">Este artigo irá mostrar como tooperform cenários comuns utilizando o armazenamento de Blobs do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90fc5-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="90fc5-106">Exemplos de Olá são escritos no Objective-C e utilizar Olá [biblioteca de clientes do Storage do Azure para iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="90fc5-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="90fc5-107">Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="90fc5-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="90fc5-108">Para obter mais informações sobre os blobs, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="90fc5-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="90fc5-109">Também pode transferir Olá [aplicação de exemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly Consulte Olá a utilização do Storage do Azure numa aplicação iOS.</span><span class="sxs-lookup"><span data-stu-id="90fc5-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="90fc5-110">Importar a biblioteca de iOS Olá Storage do Azure na sua aplicação</span><span class="sxs-lookup"><span data-stu-id="90fc5-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="90fc5-111">É possível importar biblioteca de iOS Olá Storage do Azure na sua aplicação utilizando Olá [CocoaPod de armazenamento do Azure](https://cocoapods.org/pods/AZSClient) ou importando Olá **Framework** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="90fc5-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="90fc5-112">CocoaPod é Olá recomendado a forma como os facilita a biblioteca de Olá integrar, no entanto a importação Olá framework ficheiro é menos intrusivo para o seu projeto existente.</span><span class="sxs-lookup"><span data-stu-id="90fc5-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="90fc5-113">toouse nesta biblioteca, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="90fc5-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="90fc5-114">iOS 8 +</span><span class="sxs-lookup"><span data-stu-id="90fc5-114">iOS 8+</span></span>
- <span data-ttu-id="90fc5-115">Xcode 7 +</span><span class="sxs-lookup"><span data-stu-id="90fc5-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="90fc5-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="90fc5-116">CocoaPod</span></span>
1. <span data-ttu-id="90fc5-117">Se ainda não o fez, por isso, já, [instalar o CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) no seu computador, abra uma janela de terminal e Olá os seguintes comandos a executar</span><span class="sxs-lookup"><span data-stu-id="90fc5-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="90fc5-118">Em seguida, no diretório de projeto Olá (diretório de Olá que contém o ficheiro xcodeproj), crie um novo ficheiro chamado _Podfile_(extensão de ficheiro).</span><span class="sxs-lookup"><span data-stu-id="90fc5-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="90fc5-119">Adicione Olá seguir too_Podfile_ e guardar.</span><span class="sxs-lookup"><span data-stu-id="90fc5-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="90fc5-120">Na janela de terminal Olá, navegue toohello diretório de projeto e Olá execute os seguintes comandos</span><span class="sxs-lookup"><span data-stu-id="90fc5-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="90fc5-121">Se a sua xcodeproj estiver aberta no Xcode, feche-o.</span><span class="sxs-lookup"><span data-stu-id="90fc5-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="90fc5-122">No seu ficheiro de projeto do projeto diretório Olá abra recém-criado que irão ter a extensão de .xcworkspace Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="90fc5-123">Este é o ficheiro de Olá que irá trabalhar a partir de agora em.</span><span class="sxs-lookup"><span data-stu-id="90fc5-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="90fc5-124">Framework</span><span class="sxs-lookup"><span data-stu-id="90fc5-124">Framework</span></span>
<span data-ttu-id="90fc5-125">Olá outra forma de biblioteca de Olá toouse é framework de Olá toobuild manualmente:</span><span class="sxs-lookup"><span data-stu-id="90fc5-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="90fc5-126">Primeiro, transferir ou Olá clone [repositório azure-storage-ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="90fc5-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="90fc5-127">Vá para *azure-storage-ios* -> *Lib* -> *biblioteca de clientes do Storage do Azure*e abra `AZSClient.xcodeproj` no Xcode.</span><span class="sxs-lookup"><span data-stu-id="90fc5-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="90fc5-128">Em Olá superior esquerdo do Xcode, alteração Olá Active Directory esquema de "Biblioteca de clientes do Storage do Azure" demasiado "Framework".</span><span class="sxs-lookup"><span data-stu-id="90fc5-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="90fc5-129">Compilar o projeto de Olá (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="90fc5-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="90fc5-130">Esta ação irá criar um `AZSClient.framework` ficheiro no seu ambiente de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90fc5-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="90fc5-131">Pode, em seguida, importar ficheiro de framework de Olá na sua aplicação, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="90fc5-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="90fc5-132">Criar um novo projeto ou abrir projeto existente no Xcode.</span><span class="sxs-lookup"><span data-stu-id="90fc5-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="90fc5-133">Arrastar e largar Olá `AZSClient.framework` para o seu navegador de projeto Xcode.</span><span class="sxs-lookup"><span data-stu-id="90fc5-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="90fc5-134">Selecione *copiar itens, se for necessário*e clique em *concluir*.</span><span class="sxs-lookup"><span data-stu-id="90fc5-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="90fc5-135">Clique no seu projeto na navegação esquerda Olá e clique em Olá *geral* separador, Olá parte superior do editor de projeto Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="90fc5-136">Em Olá *estruturas e bibliotecas ligadas* secção, clique no botão de adicionar Olá (+).</span><span class="sxs-lookup"><span data-stu-id="90fc5-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="90fc5-137">Na lista de Olá de bibliotecas que já são fornecidos, procure `libxml2.2.tbd` e adicioná-la tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="90fc5-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="90fc5-138">Importar Olá biblioteca</span><span class="sxs-lookup"><span data-stu-id="90fc5-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="90fc5-139">Se estiver a utilizar o Swift, será necessário toocreate um cabeçalho de bridging e importar < AZSClient/AZSClient.h > não existe:</span><span class="sxs-lookup"><span data-stu-id="90fc5-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="90fc5-140">Criar um ficheiro de cabeçalho `Bridging-Header.h`e adicione Olá acima declarações de importação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="90fc5-141">Aceda toohello *definições de criação* separador e procure *cabeçalho de Bridging Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="90fc5-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="90fc5-142">Faça duplo clique no campo Olá de *cabeçalho de Bridging Objective-C* e adicione o ficheiro de cabeçalho Olá caminho tooyour:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="90fc5-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="90fc5-143">Compilação Olá projeto (⌘ + B) tooverify que Olá cabeçalho de bridging foi captado pelo Xcode.</span><span class="sxs-lookup"><span data-stu-id="90fc5-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="90fc5-144">Começar a utilizar a biblioteca de Olá diretamente no ficheiro qualquer Swift, não é necessário para instruções de importação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="90fc5-145">Operações assíncronas</span><span class="sxs-lookup"><span data-stu-id="90fc5-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="90fc5-146">Todos os métodos que executam um pedido de serviço Olá são operações assíncronas.</span><span class="sxs-lookup"><span data-stu-id="90fc5-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="90fc5-147">Exemplos de código Olá, irá encontrar que estes métodos tem um processador de conclusão.</span><span class="sxs-lookup"><span data-stu-id="90fc5-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="90fc5-148">Código dentro de Olá conclusão processador será executado **depois** Olá é concluído.</span><span class="sxs-lookup"><span data-stu-id="90fc5-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="90fc5-149">Code depois Olá conclusão processador será executado **enquanto** pedido Olá está a ser efetuado.</span><span class="sxs-lookup"><span data-stu-id="90fc5-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="90fc5-150">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="90fc5-150">Create a container</span></span>
<span data-ttu-id="90fc5-151">Todos os BLOBs no armazenamento do Azure têm de residir num contentor.</span><span class="sxs-lookup"><span data-stu-id="90fc5-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="90fc5-152">Olá exemplo seguinte mostra como toocreate um contentor, designado por *newcontainer*, na sua conta de armazenamento se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="90fc5-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="90fc5-153">Ao escolher um nome para o contentor, ser mindful de Olá nomenclatura regras acima referido.</span><span class="sxs-lookup"><span data-stu-id="90fc5-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="90fc5-154">Pode confirmar que este processo funciona observando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) e verificar que *newcontainer* se encontra na lista de Olá de contentores para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="90fc5-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="90fc5-155">Definir permissões do contentor</span><span class="sxs-lookup"><span data-stu-id="90fc5-155">Set Container Permissions</span></span>
<span data-ttu-id="90fc5-156">Permissões de um contentor estão configuradas para **privada** acesso por predefinição.</span><span class="sxs-lookup"><span data-stu-id="90fc5-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="90fc5-157">No entanto, os contentores fornecem algumas opções diferentes para acesso do contentor:</span><span class="sxs-lookup"><span data-stu-id="90fc5-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="90fc5-158">**Privada**: dados blob e contentor podem ser lida por apenas o proprietário da conta Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="90fc5-159">**Blob**: dados BLOBs neste contentor podem ser lidos através do pedido anónimo, mas não estão disponíveis dados de contentor.</span><span class="sxs-lookup"><span data-stu-id="90fc5-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="90fc5-160">Os clientes não é possível enumerar os blobs no contentor de Olá através do pedido anónimo.</span><span class="sxs-lookup"><span data-stu-id="90fc5-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="90fc5-161">**Contentor**: dados blob e contentor podem ser lidos através do pedido anónimo.</span><span class="sxs-lookup"><span data-stu-id="90fc5-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="90fc5-162">Os clientes podem enumerar os blobs no contentor de Olá através do pedido anónimo, mas não é possível enumerar os contentores na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="90fc5-163">Olá exemplo seguinte mostra como toocreate um contentor com **contentor** permissões, o que lhe permitirá o acesso público só de leitura para todos os utilizadores Olá Internet de acesso:</span><span class="sxs-lookup"><span data-stu-id="90fc5-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="90fc5-164">Carregar um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="90fc5-164">Upload a blob into a container</span></span>
<span data-ttu-id="90fc5-165">Tal como mencionado na Olá [conceitos do serviço do Blob](#blob-service-concepts) secção, Blob Storage oferece três tipos diferentes de blobs: blobs de blocos, blobs de acréscimo e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="90fc5-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="90fc5-166">biblioteca de iOS Olá Storage do Azure suporta todos os três tipos de blobs.</span><span class="sxs-lookup"><span data-stu-id="90fc5-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="90fc5-167">Na maioria dos casos, o blob de bloco é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="90fc5-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="90fc5-168">Olá seguinte exemplo mostra como tooupload um bloco de blob a partir de um NSString.</span><span class="sxs-lookup"><span data-stu-id="90fc5-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="90fc5-169">Se um blob com o mesmo nome já existe neste contentor de Olá, conteúdo Olá este blob será substituído.</span><span class="sxs-lookup"><span data-stu-id="90fc5-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="90fc5-170">Pode confirmar que este processo funciona observando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) e verificar esse contentor Olá, *containerpublic*, contém Olá blob, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="90fc5-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="90fc5-171">Neste exemplo, é utilizado um contentor público para também pode verificar se esta aplicação trabalhado por vai toohello blobs URI:</span><span class="sxs-lookup"><span data-stu-id="90fc5-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="90fc5-172">Além disso toouploading um blob de blocos de um NSString, semelhantes existem métodos NSData, NSInputStream ou um ficheiro local.</span><span class="sxs-lookup"><span data-stu-id="90fc5-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="90fc5-173">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="90fc5-173">List hello blobs in a container</span></span>
<span data-ttu-id="90fc5-174">Olá exemplo seguinte mostra como toolist todos os blobs num contentor.</span><span class="sxs-lookup"><span data-stu-id="90fc5-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="90fc5-175">Quando efetuar esta operação, não mindful de Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="90fc5-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="90fc5-176">**continuationToken** -Olá representa de token de continuação onde deve começar Olá listagem a operação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="90fc5-177">Se não for fornecido nenhum token, irá listar a blobs a partir do início de Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="90fc5-178">Pode ser apresentado qualquer número de blobs, do zero se tooa definida máximo.</span><span class="sxs-lookup"><span data-stu-id="90fc5-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="90fc5-179">Mesmo que este método devolve zero resultados, se `results.continuationToken` não é nil, poderão existir mais blobs no serviço de Olá que não foi indicados.</span><span class="sxs-lookup"><span data-stu-id="90fc5-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="90fc5-180">**prefixo** -pode especificar Olá prefixo toouse para lista de blob.</span><span class="sxs-lookup"><span data-stu-id="90fc5-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="90fc5-181">Apenas os blobs que começam com este prefixo serão apresentados.</span><span class="sxs-lookup"><span data-stu-id="90fc5-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="90fc5-182">**useFlatBlobListing** - tal como mencionado na Olá [nomenclatura e referência de contentores e blobs](#naming-and-referencing-containers-and-blobs) secção, embora Olá serviço Blob é um esquema de armazenamento simples, é possível criar uma hierarquia virtual ao nomear blobs com o caminho informações.</span><span class="sxs-lookup"><span data-stu-id="90fc5-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="90fc5-183">No entanto, não plana listagem não é atualmente suportada.</span><span class="sxs-lookup"><span data-stu-id="90fc5-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="90fc5-184">Esta funcionalidade estará disponível brevemente.</span><span class="sxs-lookup"><span data-stu-id="90fc5-184">This feature is coming soon.</span></span> <span data-ttu-id="90fc5-185">Por agora, este valor deve ser **Sim**.</span><span class="sxs-lookup"><span data-stu-id="90fc5-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="90fc5-186">**blobListingDetails** -pode especificar que tooinclude de itens quando listar os blobs</span><span class="sxs-lookup"><span data-stu-id="90fc5-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="90fc5-187">_AZSBlobListingDetailsNone_: listar apenas consolidados blobs e devolve os metadados de blob.</span><span class="sxs-lookup"><span data-stu-id="90fc5-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="90fc5-188">_AZSBlobListingDetailsSnapshots_: listar blobs consolidados e instantâneos do blob.</span><span class="sxs-lookup"><span data-stu-id="90fc5-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="90fc5-189">_AZSBlobListingDetailsMetadata_: obter metadados do blob para cada blob devolvido numa listagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="90fc5-190">_AZSBlobListingDetailsUncommittedBlobs_: listar blobs consolidados e não consolidados.</span><span class="sxs-lookup"><span data-stu-id="90fc5-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="90fc5-191">_AZSBlobListingDetailsCopy_: incluir copiar propriedades numa listagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="90fc5-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="90fc5-192">_AZSBlobListingDetailsAll_: lista de todos os blobs consolidados disponíveis, não consolidados blobs e instantâneos e devolver todos os Estados de metadados e copie para os blobs.</span><span class="sxs-lookup"><span data-stu-id="90fc5-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="90fc5-193">**maxResults** -Olá número máximo de resultados tooreturn para esta operação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="90fc5-194">Utilize -1 toonot definir um limite.</span><span class="sxs-lookup"><span data-stu-id="90fc5-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="90fc5-195">**completionHandler** -bloco de Olá de código tooexecute com resultados de Olá de Olá listagem a operação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="90fc5-196">Neste exemplo, um método de programa auxiliar é o método de blobs do toorecursively utilizados chamada Olá lista sempre que é devolvido um token de continuação.</span><span class="sxs-lookup"><span data-stu-id="90fc5-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="90fc5-197">Transferir um blob</span><span class="sxs-lookup"><span data-stu-id="90fc5-197">Download a blob</span></span>
<span data-ttu-id="90fc5-198">Olá seguinte exemplo mostra como toodownload um objeto de NSString tooa blob.</span><span class="sxs-lookup"><span data-stu-id="90fc5-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="90fc5-199">Eliminar um blob</span><span class="sxs-lookup"><span data-stu-id="90fc5-199">Delete a blob</span></span>
<span data-ttu-id="90fc5-200">Olá seguinte exemplo mostra como toodelete um blob.</span><span class="sxs-lookup"><span data-stu-id="90fc5-200">hello following example shows how toodelete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="90fc5-201">Eliminar um contentor do blob</span><span class="sxs-lookup"><span data-stu-id="90fc5-201">Delete a blob container</span></span>
<span data-ttu-id="90fc5-202">Olá seguinte exemplo mostra como toodelete um contentor.</span><span class="sxs-lookup"><span data-stu-id="90fc5-202">hello following example shows how toodelete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="90fc5-203">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="90fc5-203">Next steps</span></span>
<span data-ttu-id="90fc5-204">Agora que aprendeu como toouse armazenamento de Blobs do iOS, siga estas toolearn ligações mais informações sobre a biblioteca de iOS Olá e Olá o serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="90fc5-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="90fc5-205">Biblioteca de clientes do Storage do Azure para iOS</span><span class="sxs-lookup"><span data-stu-id="90fc5-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="90fc5-206">IOS de armazenamento do Azure documentação de referência</span><span class="sxs-lookup"><span data-stu-id="90fc5-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="90fc5-207">API REST dos Serviços do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="90fc5-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="90fc5-208">Blogue da Equipa de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="90fc5-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="90fc5-209">Se tiver dúvidas sobre esta biblioteca, pode toopost livre tooour [fórum do MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="90fc5-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="90fc5-210">Se tiver sugestões de funcionalidades para o Storage do Azure, publique demasiado[comentários de armazenamento do Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="90fc5-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

