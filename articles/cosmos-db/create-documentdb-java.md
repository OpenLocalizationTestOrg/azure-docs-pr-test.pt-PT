---
title: aaaCreate uma base de dados de documento de BD do Cosmos do Azure com o Java | Microsoft Docs | Microsoft Docs
description: "Apresenta um exemplo de código Java, pode utilizar tooconnect tooand consulta Olá API de DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>BD do Azure do Cosmos: Criar uma base de dados de documento utilizando Java e Olá portal do Azure

O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente. 

Este guia de introdução cria um documento de base de dados utilizando Olá ferramentas portais do Azure para a base de dados do Azure Cosmos. Este guia de introdução mostra também como tooquickly criar uma aplicação de consola Java utilizando Olá [API de Java DocumentDB](documentdb-sdk-java.md). Olá instruções deste guia de introdução podem ser seguidas em qualquer sistema operativo que seja capaz de executar Java. Por concluir este guia de introdução estará familiarizado com a criar e modificar recursos de base de dados de documento no Olá IU ou x509securitytokenparameters, optando-se a sua preferência.

## <a name="prerequisites"></a>Pré-requisitos

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Ubuntu, executado `apt-get install default-jdk` tooinstall Olá JDK.
    * Ser tooset se Olá JAVA_HOME ambiente toopoint variável toohello pasta onde Olá JDK está instalado.
* [Transferir](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um arquivo binário [Maven](http://maven.apache.org/)
    * No Ubuntu, pode executar `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * No Ubuntu, pode executar `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de base de dados

Antes de poder criar uma base de dados de documento, terá de toocreate uma conta de base de dados SQL (DocumentDB) com base de dados do Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Adicionar dados de exemplo

Agora pode adicionar dados tooyour nova coleção com o Explorador de dados.

1. No Explorador de dados nova base de dados Olá aparece no painel de coleções de Olá. Expanda Olá **tarefas** da base de dados, expanda Olá **itens** coleção, clique em **documentos**e, em seguida, clique em **novos documentos**. 

   ![Criar novos documentos no Explorador de dados no Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Agora, adicione uma coleção de toohello documentos com Olá seguir a estrutura.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Depois de adicionar Olá json toohello **documentos** separador, clique em **guardar**.

    ![Copiar dados json e clique em Guardar no Explorador de dados no Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Criar e guardar um documento mais onde inserir um valor exclusivo para Olá `id` propriedade e alteração Olá outras propriedades como julgar. Agora, os documentos podem ter qualquer estrutura que queira criar, uma vez que o Azure Cosmos DB não impõe qualquer esquema aos seus dados.

     Pode agora utilizar as consultas no Explorador de dados tooretrieve os dados clicando Olá **Editar filtro** e **aplicar filtro** botões. Por predefinição, o Explorador de dados utiliza `SELECT * FROM c` tooretrieve todos os documentos numa coleção de Olá, mas pode alterar esse tooa diferentes [consulta SQL](documentdb-sql-query.md), tais como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de Olá por ordem descendente, com base no os seus timestamp. 
 
     Também pode utilizar os procedimentos de toocreate armazenado do Explorador de dados, UDFs e lógica de negócio do lado do servidor de tooperform de acionadores bem como o débito de escala. Explorador de dados expõe todos os Olá incorporada programático acesso aos dados disponível no Olá APIs, mas fornece acesso fácil tooyour dados no Olá portal do Azure.

## <a name="clone-hello-sample-application"></a>Aplicação de exemplo de Olá do clone

Agora vamos comutador tooworking com o código. Vamos de clone de uma aplicação API do DocumentDB a partir do GitHub, definir a cadeia de ligação de Olá e executá-la. Pode ver como é fácil toowork com dados através de programação. 

1. Abra uma janela de terminal do git, tais como o git bash, e `CD` tooa diretório de trabalho.  

2. Execute Olá repositório do comando tooclone Olá exemplo a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Rever o código de Olá

Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá. Abra Olá `Program.java` ficheiros da pasta de \src\GetStarted Olá e localizar estas linhas de código que criar Olá recursos do Azure Cosmos DB. 

* Olá `DocumentClient` está inicializado.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* É criada uma nova base de dados.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* É criada uma nova coleção.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* São criados alguns documentos.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* É feita uma consulta SQL através de JSON.

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá. Este procedimento activará a toocommunicate de aplicação com a base de dados alojada.

1. No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **chaves**e, em seguida, clique em **chaves de leitura e escrita**. Irá utilizar botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã URI e a chave primária para Olá `Program.java` ficheiro no passo seguinte Olá.

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-dotnet/keys.png)

2. No Olá abra `Program.java` ficheiro, copie o valor URI do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor Olá endpoint toohello DocumentClient o construtor no `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Em seguida, copie o valor de chave primária do portal de Olá e cole-o através de "FILLME", tornando Olá segundo parâmetro no construtor do Olá DocumentClient. Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos. 
    
## <a name="run-hello-app"></a>Executar a aplicação Olá

1. Na janela de terminal git Olá, `cd` pasta azure-cosmos-db-documentdb-java-getting-started toohello.

2. Na janela de terminal git Olá, escreva `mvn package` tooinstall Olá necessário pacotes de Java.

3. Na janela de terminal git Olá, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no Olá toostart de janela de terminal, a aplicação de Java.

    Na janela de terminal Olá, irá receber a notificação Olá FamilyDB base de dados foi criado e toopress toocontinue uma chave. Prima uma base de dados de Olá toocreate chave, em seguida, mude toohello Explorador de dados e verá que agora contém uma base de dados FamilyDB. Continuar toopress chaves toocreate Olá coleção e Olá documentos e, em seguida, executar uma consulta. Quando tiver concluído o projeto de Olá, recursos de Olá são eliminados da sua conta. 

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Reveja os SLAs no Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:

1. No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos, base de dados de documento e coleção utilizando Olá Explorador de dados e executar uma aplicação toodo Olá mesma coisa através de programação. Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais. 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md) (Importar dados para o Azure Cosmos DB).


