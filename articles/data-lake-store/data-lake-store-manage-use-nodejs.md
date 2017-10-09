---
title: aaaGet iniciado com o Azure Data Lake Store utilizando o Azure SDK para Node.js | Microsoft Docs
description: "Saiba como o sistema de ficheiros de toouse Node.js toowork com contas do Data Lake Store e Olá."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Introdução ao Azure Data Lake Store utilizando o Azure SDK para Node.js
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK do .NET](data-lake-store-get-started-net-sdk.md)
> * [SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> Para carregar e transferir grande quantidade de dados (ficheiros grandes, um grande número de ficheiros ou ambos), recomendamos que utilize Olá [Python SDK](data-lake-store-get-started-python.md), Olá [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), ou [o Azure PowerShell](data-lake-store-get-started-powershell.md). Estas opções têm um melhor desempenho como utilizarem várias movimento de dados do Olá tooparallelize threads.
> 
> 

Saiba como toouse hello do Azure SDK para Node.js toocreate uma conta do Azure Data Lake Store e executar operações básicas, tais como criar pastas, carregar e transferem ficheiros de dados, eliminar a conta, etc. Para obter mais informações sobre o Data Lake Store, veja [Descrição geral do Data Lake Store](data-lake-store-overview.md). Atualmente, hello SDK suporta a

* **Versão Node.js: 0.10.0 ou superior**
* **Versão de API REST para a Conta: 2015-10-01-preview**
* **Versão de REST API para o sistema de ficheiros: 2015-10-01-preview**

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, tem de ter o seguinte Olá:

* **Uma subscrição do Azure**. Veja [Obter versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar uma Aplicação do Azure Active Directory**. Utilizar aplicações de Data Lake Store de Olá aplicação tooauthenticate Olá do Azure AD com o Azure AD. Existem diferentes abordagens tooauthenticate com o Azure AD, que são **autenticação de utilizador final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação de utilizador final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Como tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Autenticar com o Azure Active Directory
fragmentos de Olá abaixo mostram duas formas diferentes de autenticar com o Data Lake Store através do Azure AD. Para ver um debate detalhado em vários métodos toouse para autenticação com o Data Lake Store, consulte [autenticar com o Data Lake Store utilizando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

fragmento Olá abaixo também requer entradas, como o nome de domínio do Azure AD, ID de cliente para uma aplicação do Azure AD, etc. Todos os estes detalhes podem ser obtidos a partir de uma aplicação do Azure AD tem de criar, Olá detalhes sobre que também está incluídas na ligação acima.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Criar os clientes do Olá Data Lake Store
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Data Lake Store
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a>Crie um ficheiro com o conteúdo
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a>Obter uma lista de ficheiros e pastas
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a>Consultar também
* [Microsoft Azure SDK para Node.js](https://github.com/azure/azure-sdk-for-node)
* [Microsoft Azure SDK para Node.js - gestão do Data Lake Analytics](https://www.npmjs.com/package/azure-arm-datalake-analytics)

