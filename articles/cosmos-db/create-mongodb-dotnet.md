---
title: "Azure Cosmos DB: Criar uma aplicação web com o .NET e Olá MongoDB API | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET que pode utilizar tooconnect tooand consulta Olá API do Azure Cosmos DB MongoDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>BD do Azure do Cosmos: Criar uma aplicação de web API do MongoDB com o .NET e Olá portal do Azure

O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente. 

Este guia de introdução demonstra como toocreate uma conta de base de dados do Azure Cosmos, a base de dados de documento e a coleção a utilizar Olá portal do Azure. Em seguida, irá criar e implementar uma aplicação de web de lista de tarefas incorporada no Olá [controlador MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Pré-requisitos

Se ainda não tiver o Visual Studio 2017, instalado, pode transferir e utilizar Olá **livre** [edição de Comunidade de 2017 do Visual Studio](https://www.visualstudio.com/downloads/). Certifique-se de que ativa **programação do Azure** durante a configuração do Visual Studio Olá.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Criar uma conta de base de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Aplicação de exemplo de Olá do clone

Agora vamos clone uma API de MongoDB aplicação a partir do github, definir a cadeia de ligação de Olá e executá-la. Verá como é fácil toowork com dados através de programação. 

1. Abra uma janela de terminal do git, tais como o git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório do comando tooclone Olá exemplo a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Em seguida, abra o ficheiro de solução Olá no Visual Studio. 

## <a name="review-hello-code"></a>Rever o código de Olá

Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá. Abra Olá **Dal.cs** ficheiro em Olá **DAL** directory e irá encontrar que estas linhas de código criar Olá recursos de base de dados do Azure Cosmos. 

* Inicializar Olá Mongo cliente.

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* Obter a base de dados de Olá e coleção Olá.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Obter todos os documentos.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.

1. No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **cadeia de ligação**e, em seguida, clique em **chaves de leitura e escrita**. Irá utilizar os botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã nome de utilizador, palavra-passe e o anfitrião no ficheiro de Dal.cs Olá no passo seguinte Olá.

2. Abra Olá **Dal.cs** ficheiro Olá **DAL** diretório. 

3. Copiar o **nome de utilizador** valor a partir do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor Olá **nome de utilizador** no seu **Dal.cs** ficheiro. 

4. Em seguida, copie o **anfitrião** valor a partir do portal de Olá e torná-lo Olá valor Olá **anfitrião** no seu **Dal.cs** ficheiro. 

5. Por fim, copie o **palavra-passe** valor a partir do portal de Olá e torná-lo Olá valor Olá **palavra-passe** no seu **Dal.cs** ficheiro. 

Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos. 
    
## <a name="run-hello-web-app"></a>Executar a aplicação web de Olá

1. No Visual Studio, clique com botão direito no projeto Olá no **Explorador de soluções** e, em seguida, clique em **gerir pacotes NuGet**. 

2. No Olá NuGet **procurar** caixa, escreva *MongoDB.Driver*.

3. Resultados de Olá, instalar Olá **MongoDB.Driver** biblioteca. Esta ação instala o pacote de MongoDB.Driver Olá, bem como todas as dependências.

4. Clique em CTRL + F5 aplicação de Olá toorun. A aplicação é apresentada no browser. 

5. Clique em **criar** no Olá browser e criar algumas novas tarefas na sua aplicação de lista de tarefas.

## <a name="review-slas-in-hello-azure-portal"></a>Reveja os SLAs no Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:

1. No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos e execute uma aplicação web através de hello API para MongoDB. Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais. 

> [!div class="nextstepaction"]
> [Importe dados para a base de dados do Azure Cosmos para Olá API do MongoDB](mongodb-migrate.md)

