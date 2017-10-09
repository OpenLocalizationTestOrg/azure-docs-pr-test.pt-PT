---
title: aaaHow toouse Blob storage do Node.js | Microsoft Docs
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Como toouse Blob storage do Node.js
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Descrição geral
Este artigo mostra como tooperform cenários comuns utilizando o Blob storage. Exemplos de Olá são escritos através do Olá Node.js API. cenários de Olá abrangidos incluem como tooupload, listar, transferir e eliminar blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js
Para obter instruções sobre como toocreate uma aplicação Node.js, consulte [criar uma aplicação de web de Node.js no App Service do Azure], [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) – com o Windows PowerShell, ou [compilar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess de aplicação
toouse storage do Azure, terá de Olá SDK de armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas de conveniência que comunicam com os serviços de REST de armazenamento Olá.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utilizar o Gestor de pacote de nó (NPM) tooobtain Olá pacote
1. Utilize uma interface de linha de comandos, como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), toonavigate toohello pasta onde criou o seu exemplo aplicação.
2. Tipo **npm instalar storage do azure** na janela de comandos Olá. O resultado do comando de Olá é semelhante toohello seguinte exemplo de código.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, determinar Olá **storage do azure** pacote, que contém as bibliotecas de Olá que necessita de armazenamento tooaccess.

### <a name="import-hello-package"></a>Importar o pacote de Olá
Utilizar o bloco de notas ou noutro editor de texto, adicionar Olá seguir toohello superior de Olá **server.js** ficheiro da aplicação olá onde pretende toouse armazenamento:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma ligação de armazenamento do Azure
Olá módulo do Azure será lida a variáveis de ambiente de Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, para as informações necessárias tooconnect tooyour conta de armazenamento Azure. Se estas variáveis de ambiente não estiver definidas, tem de especificar as informações da conta Olá ao chamar **createBlobService**.

Para obter um exemplo de definir variáveis de ambiente de Olá na Olá [portal do Azure](https://portal.azure.com) para uma aplicação web do Azure, consulte [através da aplicação de web de Node.js Olá o serviço de tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-container"></a>Criar um contentor
Olá **BlobService** objeto permite-lhe trabalhar com blobs e contentores. Olá código seguinte cria um **BlobService** objeto. Adicione Olá seguinte perto da parte superior Olá **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Pode aceder anonimamente um blob utilizando **createBlobServiceAnonymous** e fornecer o endereço do anfitrião Olá. Por exemplo, utilizar `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

toocreate um novo contentor, utilize **createContainerIfNotExists**. Olá exemplo de código seguinte cria um novo contentor designado 'mycontainer':

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Se o contentor de Olá é criado recentemente, `result.created` é verdadeiro. Se já existir um contentor de Olá, `result.created` é falso. `response`contém informações sobre a operação de Olá, incluindo Olá ETag informações para o contentor de Olá.

### <a name="container-security"></a>Segurança de contentor
Por predefinição, os novos contentores são privados e não podem ser acedidos anonimamente. contentor de Olá toomake pública para que possam aceder anonimamente, pode definir o nível de acesso de um contentor Olá demasiado**blob** ou **contentor**.

* **blob** -permite o acesso de leitura anónimo tooblob conteúdo e metadados dentro neste contentor, mas não toocontainer metadados, tais como listar todos os blobs num contentor
* **contentor** -permite o acesso de leitura anónimo tooblob conteúdo e metadados, bem como metadados do contentor

Olá exemplo de código seguinte demonstra um nível de acesso Olá definição demasiado**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Em alternativa, pode modificar o nível de acesso de Olá de um contentor utilizando **setContainerAcl** nível de acesso de Olá toospecify. toocontainer ao nível do exemplo alterações Olá acesso de código seguinte Olá:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Olá resultado contém informações sobre a operação de Olá, incluindo Olá atual **ETag** para o contentor de Olá.

### <a name="filters"></a>Filtros
Pode aplicar opcional filtragem operações toooperations efetuada utilizando **BlobService**. Operações de filtragem pode incluir registo automaticamente repetir, etc. Os filtros são objetos que implementam um método com assinatura de Olá:

```nodejs
function handle (requestOptions, next)
```

Depois de efetuar a respetiva pré-processamentos nas opções de pedido de Olá, Olá método necessita toocall "seguinte", transmitir uma chamada de retorno com Olá assinatura os seguintes:

```nodejs
function (returnObject, finalCallback, next)
```

Esta chamada de retorno e após o processamento Olá returnObject (resposta de hello do servidor de toohello Olá pedido), a chamada de retorno de Olá tem tooeither invocar em seguida, se existir toocontinue outros filtros de processamento ou simplesmente invocar o serviço de Olá finalCallback tooend invocação.

Dois filtros que implementa lógica de repetição são incluídos com Olá Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. seguinte Olá cria um **BlobService** objeto que utiliza Olá **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
Existem três tipos de blobs: blobs de blocos, blobs de páginas e blobs de acréscimo. Os blobs de blocos permitem-lhe toomore eficientemente carregar dados de grandes dimensões. Acrescentar blobs estão otimizados para operações de acréscimo. Os blobs de página estão otimizados para operações de leitura/escrita. Para obter mais informações, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Blobs de bloco
blob de bloco de tooa por dados tooupload, Olá utilize os seguintes:

* **createBlockBlobFromLocalFile** - cria um novo blob de bloco e carrega Olá conteúdo de um ficheiro
* **createBlockBlobFromStream** - cria um novo blob de bloco e carrega o conteúdo de Olá de um fluxo
* **createBlockBlobFromText** - cria um novo blob de bloco e carrega o conteúdo de Olá de uma cadeia
* **createWriteStreamToBlockBlob** -fornece um blob de bloco de tooa de fluxo de escrita

Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Olá `result` devolvido por estes métodos contém informações sobre a operação de Olá, tais como Olá **ETag** do blob Olá.

### <a name="append-blobs"></a>Blobs de acréscimo
tooupload dados tooa novo blob de acréscimo, utilize Olá seguinte:

* **createAppendBlobFromLocalFile** - cria um novo blob de acréscimo e carrega Olá conteúdo de um ficheiro
* **createAppendBlobFromStream** - cria um novo blob de acréscimo e carrega o conteúdo de Olá de um fluxo
* **createAppendBlobFromText** - cria um novo blob de acréscimo e carrega o conteúdo de Olá de uma cadeia
* **createWriteStreamToNewAppendBlob** - cria um novo blob de acréscimo e, em seguida, fornece uma tooit toowrite de fluxo

Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend existente de tooan um bloco acrescentar blob, Olá utilize os seguintes:

* **appendFromLocalFile** -acrescentar conteúdo Olá de um ficheiro tooan existente Acrescentar blob
* **appendFromStream** -acrescentar conteúdo Olá de um fluxo tooan existente Acrescentar blob
* **appendFromText** -acrescentar conteúdo Olá de uma cadeia tooan existente Acrescentar blob
* **appendBlockFromStream** -acrescentar conteúdo Olá de um fluxo tooan existente Acrescentar blob
* **appendBlockFromText** -acrescentar conteúdo Olá de uma cadeia tooan existente Acrescentar blob

> [!NOTE]
> appendFromXXX APIs irá efetuar algumas chamadas de servidor desnecessários do lado do cliente validação toofail tooavoid rápida. appendBlockFromXXX não.
>
>

Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Blobs de páginas
blob de páginas de tooa por dados tooupload, Olá utilize os seguintes:

* **createPageBlob** -cria um novo blob de página com um comprimento específico
* **createPageBlobFromLocalFile** - cria um novo blob de página e carrega Olá conteúdo de um ficheiro
* **createPageBlobFromStream** - cria um novo blob de página e carrega o conteúdo de Olá de um fluxo
* **createWriteStreamToExistingPageBlob** -fornece um blob de página existente do escrita fluxo tooan
* **createWriteStreamToNewPageBlob** - cria um novo blob de página e, em seguida, fornece uma tooit toowrite de fluxo

Olá exemplo de código seguinte carrega conteúdo Olá Olá **test.txt** de ficheiros para **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Os blobs de páginas consistem de 512 bytes 'páginas'. Receberá um erro ao carregar dados com um tamanho que não é um múltiplo de 512.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
os blobs de Olá toolist num contentor, utilize Olá **listBlobsSegmented** método. Se gostaria de blobs de tooreturn com um prefixo específico, utilize **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Olá `result` contém um `entries` coleção, o que é uma matriz de objetos que descrevem cada blob. Se não não possível devolver todos os blobs, Olá `result` também fornece um `continuationToken`, que pode ser utilizado como Olá segundo parâmetro tooretrieve entradas adicionais.

## <a name="download-blobs"></a>Transferir blobs
dados toodownload de um blob, utilize o seguinte Olá:

* **getBlobToLocalFile** -escreve toofile de conteúdo de blob Olá
* **getBlobToStream** -escreve o fluxo de tooa de conteúdo de blob Olá
* **getBlobToText** -escreve conteúdos do blob Olá tooa cadeia
* **createReadStream** -fornece uma tooread fluxo a partir do blob Olá

Olá exemplo de código seguinte demonstra utilizando **getBlobToStream** conteúdo Olá toodownload Olá **myblob** blob e armazená-las toohello **output.txt** ficheiros utilizando um sequência:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Olá `result` contém informações sobre blob Olá, incluindo **ETag** informações.

## <a name="delete-a-blob"></a>Eliminar um blob
Por fim, toodelete um blob, chamar **deleteBlob**. Olá seguinte exemplo de código elimina Olá blob com o nome **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Acesso simultâneo
toosupport acesso simultâneo tooa blob a partir da vários clientes ou de múltiplas instâncias do processo, pode utilizar **ETags** ou **concessões**.

* **ETag** -fornece uma forma toodetect que Olá blob ou contentor foi modificado por outro processo
* **Concessão** - fornece uma forma tooobtain exclusivo, renováveis, operação de escrita ou eliminar o blob de tooa de acesso para um período de tempo

### <a name="etag"></a>ETag
Utilize ETags se precisar de tooallow vários clientes ou instâncias toowrite toohello bloco Blob de página ou Blob em simultâneo. Olá ETag permite-lhe toodetermine se hello contentor ou um blob foi modificada uma vez que inicialmente ler ou criou, permitindo-lhe tooavoid substituir alterações consolidadas por outro processo ou cliente.

Pode definir condições de ETag utilizando Olá opcional `options.accessConditions` parâmetro. Olá exemplo de código seguinte apenas carrega Olá **test.txt** ficheiro se blob Olá já existe e tem um valor ETag Olá contido `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Quando estiver a utilizar ETags, padrão geral Olá é:

1. Obter Olá ETag como resultado de Olá de uma operação get, a lista ou a criar.
2. Efetuar uma ação, a verificação que Olá valor ETag não foi modificada.

Se o valor de Olá foi modificado, indica que o se outra instância ou cliente modificadas blob Olá ou contentor, uma vez que obteve valor ETag de Olá.

### <a name="lease"></a>Concessão
Pode adquirir uma concessão de novo utilizando Olá **acquireLease** método, especificando blob Olá ou contentor que pretende tooobtain uma concessão no. Por exemplo, Olá seguinte código adquire uma concessão no **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Operações subsequentes no **myblob** tem de fornecer Olá `options.leaseId` parâmetro. concessão de Olá ID é devolvido como `result.id` de **acquireLease**.

> [!NOTE]
> Por predefinição, a duração da concessão Olá é infinita. Pode especificar um período de tempo infinito não (entre 15 e 60 segundos), fornecendo Olá `options.leaseDuration` parâmetro.
>
>

utilizar tooremove uma concessão **releaseLease**. toobreak uma concessão, impedir a outras pessoas, mas a partir de obter uma concessão novo até duração original Olá expirou, utilize **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Trabalhar com assinaturas de acesso partilhado
Assinaturas de acesso partilhado (SAS) são uma tooblobs de acesso granulares de tooprovide de forma segura e contentores sem fornecer o nome da conta de armazenamento ou chaves. Assinaturas de acesso partilhado são frequentemente utilizados tooprovide limitada para aceder a dados tooyour, tais como permitir que uma aplicação móvel tooaccess blobs.

> [!NOTE]
> Enquanto pode também autorizar o acesso anónimo tooblobs, assinaturas de acesso partilhado permitem-lhe acesso tooprovide mais controlado, como tem de gerar Olá SAS.
>
>

Uma aplicação como um serviço baseado na nuvem fidedigna gera assinaturas de acesso partilhado com Olá **generateSharedAccessSignature** de Olá **BlobService**e fornece-tooan não fidedigno ou fidedigna por aplicação, tais como uma aplicação móvel. Acesso partilhado assinaturas são geradas através de uma política, que descreve o início de Olá e datas final durante o qual Olá assinaturas de acesso partilhado são válidas, assim como Olá aceder nível titular de assinaturas de acesso partilhado do toohello concedida.

Olá exemplo de código seguinte gera uma nova política de acesso partilhado, o que permite Olá as operações de leitura tooperform de marcador de posição de assinaturas de acesso de Olá partilhado **myblob** blob e expira 100 minutos após a hora de Olá é criado.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Tenha em atenção que as informações do anfitrião Olá têm de ser fornecidos também, conforme necessário, quando marcador de posição de assinaturas de acesso partilhado de Olá tenta contentor de Olá tooaccess.

Olá, em seguida, a aplicação de cliente utiliza assinaturas de acesso partilhado com **BlobServiceWithSAS** tooperform operações contra blob Olá. Olá seguinte obtém as informações **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Uma vez que as assinaturas de acesso partilhado de Olá foram geradas com acesso só de leitura, se for feita uma tentativa de blob de Olá toomodify, será devolvido um erro.

### <a name="access-control-lists"></a>Lista de controlo de acesso
Também pode utilizar uma política de acesso do acesso Controlo lista (ACL) tooset Olá para SAS. Isto é útil se desejar tooallow vários clientes tooaccess um contentor, mas fornecem as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada com uma matriz de políticas de acesso, com um ID associado a cada política. Olá seguinte exemplo de código define duas políticas, uma para 'user1' e outra para 'Utilizador2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá seguinte obtém de exemplo de código Olá ACL atual para **mycontainer**e, em seguida, adiciona novas políticas de Olá utilizando **setBlobAcl**. Esta abordagem permite:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL é definida, pode, em seguida, criar com base no ID de Olá para uma política de assinaturas de acesso partilhado. Olá seguinte exemplo de código cria novas assinaturas de acesso partilhado para 'Utilizador2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá os seguintes recursos.

* [Storage do azure SDK para o nó a referência da API] [Storage do azure SDK para o nó a referência da API]
* [Blogue da equipa de armazenamento do azure] [Blogue da equipa de armazenamento do azure]
* [SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub
* [Centro para Programadores do Node.js](https://azure.microsoft.com/develop/nodejs/)
* [Transferência de dados com Olá utilitário de linha de comandos AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Aplicação de web do node.js utilizando Olá serviço de tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[Criar e implementar uma aplicação de web Node.js tooAzure utilizando a Web Matrix]: https://www.microsoft.com/web/webmatrix/  
[Utilizando Olá REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [portal do Azure]: https://portal.azure.com [criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [blogue da equipa de armazenamento do Azure]: http:// blogs.msdn.com/b/windowsazurestorage/ [Storage do Azure SDK para o nó a referência da API]: http://dl.windowsazure.com/nodestoragedocs/index.html
