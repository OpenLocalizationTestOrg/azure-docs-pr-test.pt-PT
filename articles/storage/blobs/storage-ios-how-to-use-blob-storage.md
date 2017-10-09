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
# <a name="how-toouse-blob-storage-from-ios"></a>Como toouse Blob storage do iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Este artigo irá mostrar como tooperform cenários comuns utilizando o armazenamento de Blobs do Microsoft Azure. Exemplos de Olá são escritos no Objective-C e utilizar Olá [biblioteca de clientes do Storage do Azure para iOS](https://github.com/Azure/azure-storage-ios). Olá os cenários abrangidos incluem **carregar**, **listagem**, **transferir**, e **eliminar** blobs. Para obter mais informações sobre os blobs, consulte Olá [passos](#next-steps) secção. Também pode transferir Olá [aplicação de exemplo](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly Consulte Olá a utilização do Storage do Azure numa aplicação iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Importar a biblioteca de iOS Olá Storage do Azure na sua aplicação
É possível importar biblioteca de iOS Olá Storage do Azure na sua aplicação utilizando Olá [CocoaPod de armazenamento do Azure](https://cocoapods.org/pods/AZSClient) ou importando Olá **Framework** ficheiro. CocoaPod é Olá recomendado a forma como os facilita a biblioteca de Olá integrar, no entanto a importação Olá framework ficheiro é menos intrusivo para o seu projeto existente.

toouse nesta biblioteca, terá de Olá seguintes:
- iOS 8 +
- Xcode 7 +

## <a name="cocoapod"></a>CocoaPod
1. Se ainda não o fez, por isso, já, [instalar o CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) no seu computador, abra uma janela de terminal e Olá os seguintes comandos a executar
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Em seguida, no diretório de projeto Olá (diretório de Olá que contém o ficheiro xcodeproj), crie um novo ficheiro chamado _Podfile_(extensão de ficheiro). Adicione Olá seguir too_Podfile_ e guardar.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Na janela de terminal Olá, navegue toohello diretório de projeto e Olá execute os seguintes comandos

    ```shell    
    pod install
    ```

4. Se a sua xcodeproj estiver aberta no Xcode, feche-o. No seu ficheiro de projeto do projeto diretório Olá abra recém-criado que irão ter a extensão de .xcworkspace Olá. Este é o ficheiro de Olá que irá trabalhar a partir de agora em.

## <a name="framework"></a>Framework
Olá outra forma de biblioteca de Olá toouse é framework de Olá toobuild manualmente:

1. Primeiro, transferir ou Olá clone [repositório azure-storage-ios](https://github.com/azure/azure-storage-ios).
2. Vá para *azure-storage-ios* -> *Lib* -> *biblioteca de clientes do Storage do Azure*e abra `AZSClient.xcodeproj` no Xcode.
3. Em Olá superior esquerdo do Xcode, alteração Olá Active Directory esquema de "Biblioteca de clientes do Storage do Azure" demasiado "Framework".
4. Compilar o projeto de Olá (⌘ + B). Esta ação irá criar um `AZSClient.framework` ficheiro no seu ambiente de trabalho.

Pode, em seguida, importar ficheiro de framework de Olá na sua aplicação, Olá seguinte:

1. Criar um novo projeto ou abrir projeto existente no Xcode.
2. Arrastar e largar Olá `AZSClient.framework` para o seu navegador de projeto Xcode.
3. Selecione *copiar itens, se for necessário*e clique em *concluir*.
4. Clique no seu projeto na navegação esquerda Olá e clique em Olá *geral* separador, Olá parte superior do editor de projeto Olá.
5. Em Olá *estruturas e bibliotecas ligadas* secção, clique no botão de adicionar Olá (+).
6. Na lista de Olá de bibliotecas que já são fornecidos, procure `libxml2.2.tbd` e adicioná-la tooyour projeto.

## <a name="import-hello-library"></a>Importar Olá biblioteca 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Se estiver a utilizar o Swift, será necessário toocreate um cabeçalho de bridging e importar < AZSClient/AZSClient.h > não existe:

1. Criar um ficheiro de cabeçalho `Bridging-Header.h`e adicione Olá acima declarações de importação.
2. Aceda toohello *definições de criação* separador e procure *cabeçalho de Bridging Objective-C*.
3. Faça duplo clique no campo Olá de *cabeçalho de Bridging Objective-C* e adicione o ficheiro de cabeçalho Olá caminho tooyour:`ProjectName/Bridging-Header.h`
4. Compilação Olá projeto (⌘ + B) tooverify que Olá cabeçalho de bridging foi captado pelo Xcode.
5. Começar a utilizar a biblioteca de Olá diretamente no ficheiro qualquer Swift, não é necessário para instruções de importação.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Operações assíncronas
> [!NOTE]
> Todos os métodos que executam um pedido de serviço Olá são operações assíncronas. Exemplos de código Olá, irá encontrar que estes métodos tem um processador de conclusão. Código dentro de Olá conclusão processador será executado **depois** Olá é concluído. Code depois Olá conclusão processador será executado **enquanto** pedido Olá está a ser efetuado.
> 
> 

## <a name="create-a-container"></a>Criar um contentor
Todos os BLOBs no armazenamento do Azure têm de residir num contentor. Olá exemplo seguinte mostra como toocreate um contentor, designado por *newcontainer*, na sua conta de armazenamento se ainda não existir. Ao escolher um nome para o contentor, ser mindful de Olá nomenclatura regras acima referido.

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

Pode confirmar que este processo funciona observando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) e verificar que *newcontainer* se encontra na lista de Olá de contentores para a sua conta de armazenamento.

## <a name="set-container-permissions"></a>Definir permissões do contentor
Permissões de um contentor estão configuradas para **privada** acesso por predefinição. No entanto, os contentores fornecem algumas opções diferentes para acesso do contentor:

* **Privada**: dados blob e contentor podem ser lida por apenas o proprietário da conta Olá.
* **Blob**: dados BLOBs neste contentor podem ser lidos através do pedido anónimo, mas não estão disponíveis dados de contentor. Os clientes não é possível enumerar os blobs no contentor de Olá através do pedido anónimo.
* **Contentor**: dados blob e contentor podem ser lidos através do pedido anónimo. Os clientes podem enumerar os blobs no contentor de Olá através do pedido anónimo, mas não é possível enumerar os contentores na conta do storage Olá.

Olá exemplo seguinte mostra como toocreate um contentor com **contentor** permissões, o que lhe permitirá o acesso público só de leitura para todos os utilizadores Olá Internet de acesso:

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

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
Tal como mencionado na Olá [conceitos do serviço do Blob](#blob-service-concepts) secção, Blob Storage oferece três tipos diferentes de blobs: blobs de blocos, blobs de acréscimo e blobs de páginas. biblioteca de iOS Olá Storage do Azure suporta todos os três tipos de blobs. Na maioria dos casos, o blob de bloco é Olá recomendado toouse de tipo.

Olá seguinte exemplo mostra como tooupload um bloco de blob a partir de um NSString. Se um blob com o mesmo nome já existe neste contentor de Olá, conteúdo Olá este blob será substituído.

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

Pode confirmar que este processo funciona observando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com) e verificar esse contentor Olá, *containerpublic*, contém Olá blob, *sampleblob*. Neste exemplo, é utilizado um contentor público para também pode verificar se esta aplicação trabalhado por vai toohello blobs URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

Além disso toouploading um blob de blocos de um NSString, semelhantes existem métodos NSData, NSInputStream ou um ficheiro local.

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
Olá exemplo seguinte mostra como toolist todos os blobs num contentor. Quando efetuar esta operação, não mindful de Olá os seguintes parâmetros:     

* **continuationToken** -Olá representa de token de continuação onde deve começar Olá listagem a operação. Se não for fornecido nenhum token, irá listar a blobs a partir do início de Olá. Pode ser apresentado qualquer número de blobs, do zero se tooa definida máximo. Mesmo que este método devolve zero resultados, se `results.continuationToken` não é nil, poderão existir mais blobs no serviço de Olá que não foi indicados.
* **prefixo** -pode especificar Olá prefixo toouse para lista de blob. Apenas os blobs que começam com este prefixo serão apresentados.
* **useFlatBlobListing** - tal como mencionado na Olá [nomenclatura e referência de contentores e blobs](#naming-and-referencing-containers-and-blobs) secção, embora Olá serviço Blob é um esquema de armazenamento simples, é possível criar uma hierarquia virtual ao nomear blobs com o caminho informações. No entanto, não plana listagem não é atualmente suportada. Esta funcionalidade estará disponível brevemente. Por agora, este valor deve ser **Sim**.
* **blobListingDetails** -pode especificar que tooinclude de itens quando listar os blobs
  * _AZSBlobListingDetailsNone_: listar apenas consolidados blobs e devolve os metadados de blob.
  * _AZSBlobListingDetailsSnapshots_: listar blobs consolidados e instantâneos do blob.
  * _AZSBlobListingDetailsMetadata_: obter metadados do blob para cada blob devolvido numa listagem de Olá.
  * _AZSBlobListingDetailsUncommittedBlobs_: listar blobs consolidados e não consolidados.
  * _AZSBlobListingDetailsCopy_: incluir copiar propriedades numa listagem de Olá.
  * _AZSBlobListingDetailsAll_: lista de todos os blobs consolidados disponíveis, não consolidados blobs e instantâneos e devolver todos os Estados de metadados e copie para os blobs.
* **maxResults** -Olá número máximo de resultados tooreturn para esta operação. Utilize -1 toonot definir um limite.
* **completionHandler** -bloco de Olá de código tooexecute com resultados de Olá de Olá listagem a operação.

Neste exemplo, um método de programa auxiliar é o método de blobs do toorecursively utilizados chamada Olá lista sempre que é devolvido um token de continuação.

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

## <a name="download-a-blob"></a>Transferir um blob
Olá seguinte exemplo mostra como toodownload um objeto de NSString tooa blob.

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

## <a name="delete-a-blob"></a>Eliminar um blob
Olá seguinte exemplo mostra como toodelete um blob.

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

## <a name="delete-a-blob-container"></a>Eliminar um contentor do blob
Olá seguinte exemplo mostra como toodelete um contentor.

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

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu como toouse armazenamento de Blobs do iOS, siga estas toolearn ligações mais informações sobre a biblioteca de iOS Olá e Olá o serviço de armazenamento.

* [Biblioteca de clientes do Storage do Azure para iOS](https://github.com/azure/azure-storage-ios)
* [IOS de armazenamento do Azure documentação de referência](http://azure.github.io/azure-storage-ios/)
* [API REST dos Serviços do Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blogue da Equipa de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage)

Se tiver dúvidas sobre esta biblioteca, pode toopost livre tooour [fórum do MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Se tiver sugestões de funcionalidades para o Storage do Azure, publique demasiado[comentários de armazenamento do Azure](https://feedback.azure.com/forums/217298-storage/).

