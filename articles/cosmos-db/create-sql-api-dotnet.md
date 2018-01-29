---
title: "Azure Cosmos DB: criar uma aplicação Web com .NET e a SQL API | Microsoft Docs"
description: "Apresenta um exemplo de código .NET que pode utilizar para ligar e consultar a Azure Cosmos DB SQL API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc, devcenter
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 12/15/2017
ms.author: mimig
ms.openlocfilehash: 9541fa7331a5a6a5a5405244dd79eb8a92d96386
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-build-a-sql-api-web-app-with-net-and-the-azure-portal"></a>Azure Cosmos DB: criar uma aplicação Web da SQL API com .NET e o portal do Azure

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)] 

O Azure Cosmos DB é um serviço de base de dados com vários modelos e de distribuição global da Microsoft. Pode criar e consultar rapidamente o documento, a chave/valor e as bases de dados de gráficos, que beneficiam de capacidades de escalamento horizontal e distribuição global no centro do Azure Cosmos DB. 

Este guia de introdução demonstra como criar uma conta do Azure Cosmos DB, bases de dados de documentos e coleções com o portal do Azure. Depois, vai criar e implementar uma aplicação Web de Lista A Fazer criada com a [SQL .NET API](sql-api-sdk-dotnet.md), conforme mostrado na captura de ecrã seguinte. 

![Aplicação de Lista A Fazer com dados de exemplo](./media/create-sql-api-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Pré-requisitos

Se ainda não tiver o Visual Studio 2017 instalado, pode transferir e utilizar a [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) **gratuita**. Confirme que ativa o **desenvolvimento do Azure** durante a configuração do Visual Studio.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]  

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Criar uma conta de base de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Adicionar dados de exemplo

Pode agora utilizar o Data Explorer para adicionar dados à sua coleção nova.

1. No Data Explorer, a base de dados nova aparece no painel Coleções. Expanda a base de dados **Tarefas**, expanda a coleção **Itens**, clique em **Documentos** e clique em **Documentos Novos**. 

   ![Criar documentos novos no Data Explorer no portal do Azure](./media/create-sql-api-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Agora, adicione um documento à coleção com a seguinte estrutura.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Depois de ter adicionado o json ao separador **Documentos**, clique em **Guardar**.

    ![Copie os dados json e clique em Guardar no Data Explorer no portal do Azure](./media/create-sql-api-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Crie e guarde mais um documento onde insere um valor exclusivo para a propriedade `id` e altere as outras propriedades conforme necessário. Agora, os documentos podem ter qualquer estrutura que queira criar, uma vez que o Azure Cosmos DB não impõe qualquer esquema aos seus dados.

     Pode utilizar agora consultas no Data Explorer para obter os seus dados. Por predefinição, o Data Explorer utiliza `SELECT * FROM c` para obter todos os documentos da coleção, mas pode alterar para uma [consulta SQL](sql-api-sql-query.md) diferente, como `SELECT * FROM c ORDER BY c._ts DESC`, de modo a devolver todos os documentos por ordem descendente com base no carimbo de data/hora.
 
     Também pode utilizar o Data Explorer para criar procedimentos armazenados, UDFs e acionadores, para realizar lógica empresarial do lado do servidor, bem como débito de escala. O Data Explorer expõe todos os acessos a dados programáticos incorporados que estão disponíveis nas APIs, mas disponibiliza acesso fácil aos seus dados no portal do Azure.

## <a name="clone-the-sample-application"></a>Clonar a aplicação de exemplo

Agora, vamos trabalhar com código. Vamos clonar uma aplicação da SQL API a partir do GitHub, definir a cadeia de ligação e executá-la. Vai ver como é fácil trabalhar com dados programaticamente. 

1. Abra uma janela de terminal do git, tal como git bash, e `CD` para um diretório de trabalho.  

2. Execute o seguinte comando para clonar o repositório de exemplo. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Em seguida, abra o ficheiro da solução de lista a fazer no Visual Studio. 

## <a name="review-the-code"></a>Rever o código

Vamos fazer uma breve revisão do que está a acontecer à aplicação. Abra o ficheiro DocumentDBRepository.cs e verá que estas linhas de código criam os recursos do Azure Cosmos DB. 

* O DocumentClient é inicializado na linha 78.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
    ```

* É criada uma nova base de dados na linha 93.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* É criada uma nova coleção na linha 112.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new DocumentCollection
            {
               Id = CollectionId,
               PartitionKey = new PartitionKeyDefinition() { Paths = new Collection<string>() { "/category" } }
            },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

Agora, regresse ao portal do Azure para obter as informações da cadeia de ligação e copie-as para a aplicação.

1. No [portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, na navegação da esquerda, clique em **Chaves** e em **Chaves de leitura/escrita**. Vai utilizar os botões de copiar no lado direito do ecrã para copiar o URI e a Chave Primária para o ficheiro web.config no próximo passo.

    ![Ver e copiar uma chave de acesso no portal do Azure, painel Chaves](./media/create-sql-api-dotnet/keys.png)

2. No Visual Studio 2017, abra o ficheiro web.config. 

3. Copie o valor do URI a partir do portal (com o botão Copiar) e faça deste o valor da chave do ponto final em web.config. 

    `<add key="endpoint" value="FILLME" />`

4. Em seguida, copie o valor de CHAVE PRIMÁRIA do portal e faça do mesmo o valor de authKey em web.config. Atualizou agora a sua aplicação com todas as informações necessárias para comunicar com o Azure Cosmos DB. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a>Executar a aplicação Web
1. No Visual Studio, clique com o botão direito do rato no projeto no **Explorador de Soluções** e clique em **Gerir Pacotes NuGet**. 

2. Na caixa **Procurar** do NuGet, escreva *DocumentDB*.

3. Nos resultados, instale a biblioteca **Microsoft.Azure.DocumentDB**. Esta ação instala o pacote Microsoft.Azure.DocumentDB, bem como as dependências.

4. Clique em CTRL + F5 para executar a aplicação. A aplicação é apresentada no browser. 

5. Clique em **Criar nova** no browser e crie algumas tarefas novas na aplicação Lista a Fazer.

   ![Aplicação de Lista A Fazer com dados de exemplo](./media/create-sql-api-dotnet/azure-comosdb-todo-app-list.png)

Agora, pode voltar ao Data Explorer e ver, consultar, modificar e trabalhar com estes dados novos. 

## <a name="review-slas-in-the-azure-portal"></a>Rever os SLAs no portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se não pretender continuar a utilizar esta aplicação, elimine todos os recursos criados com este guia de introdução no portal do Azure com os seguintes passos:

1. No menu do lado esquerdo do portal do Azure, clique em **Grupos de recursos** e, em seguida, clique no nome de recurso que criou. 
2. Na página do grupo de recursos, clique em **Eliminar**, escreva o nome do recurso a eliminar na caixa de texto e, em seguida, clique em **Eliminar**.

## <a name="next-steps"></a>Passos seguintes

Neste guia rápido, aprendeu a criar uma conta do Azure Cosmos DB, a criar uma coleção com o Data Explorer e a executar uma aplicação Web. Agora, pode importar dados adicionais à sua conta do Cosmos DB. 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md) (Importar dados para o Azure Cosmos DB).


