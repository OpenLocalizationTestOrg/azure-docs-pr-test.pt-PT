---
title: "Azure Cosmos DB: Criar uma aplicação com o Node.js e Olá DocumentDB API | Microsoft Docs"
description: "Apresenta um exemplo de código Node.js, pode utilizar tooconnect tooand consulta Olá API de DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>BD do Azure do Cosmos: Criar uma aplicação API do DocumentDB com o Node.js e Olá portal do Azure

O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente. 

Este guia de introdução demonstra como toocreate uma conta de base de dados do Azure Cosmos, a base de dados de documento e a coleção a utilizar Olá portal do Azure. Em seguida, criar e executar uma aplicação de consola incorporada no Olá [DocumentDB Node.js API](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Pré-requisitos

* Antes de poder executar este exemplo, tem de ter Olá os seguintes pré-requisitos:
    * Versão de [Node.js](https://nodejs.org/en/) v0.10.29 ou superior
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de base de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Aplicação de exemplo de Olá do clone

Agora vamos aplicação clone uma API de DocumentDB a partir do github, definir a cadeia de ligação de Olá e executá-la. Pode ver como é fácil toowork com dados através de programação. 

1. Abra uma janela de terminal do git, tais como o git bash, e `CD` tooa diretório de trabalho.  

2. Execute Olá repositório do comando tooclone Olá exemplo a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Rever o código de Olá

Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá. Abra Olá `app.js` ficheiro e localizar que estas linhas de código criar Olá recursos do Azure Cosmos DB. 

* Olá `documentClient` está inicializado.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* É criada uma nova base de dados.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* É criada uma nova coleção.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* São criados alguns documentos.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* É feita uma consulta SQL através de JSON.

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

Agora, volte atrás toohello tooget portal do Azure que as informações de cadeia de ligação e copie-o para a aplicação Olá.

1. No Olá [portal do Azure](http://portal.azure.com/), no seu Azure Cosmos DB conta, na Olá deixado navegação clique **chaves**e, em seguida, clique em **chaves de leitura e escrita**. Irá utilizar botões de cópia de Olá no lado direito de Olá de Olá de toocopy Olá ecrã URI e a chave primária para Olá `config.js` ficheiro no passo seguinte Olá.

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-documentdb-dotnet/keys.png)

2. No Olá abra `config.js` ficheiro. 

3. Copie o valor URI do portal de Olá (utilizando o botão de copiar Olá) e torná-lo Olá valor da chave de ponto final de Olá no `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Em seguida, copie o valor de chave primária do portal de Olá e torná-lo Olá valor Olá `config.primaryKey` no `config.js`. Agora atualizou a sua aplicação com todas as informações de Olá tem toocommunicate com base de dados do Azure Cosmos. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Executar a aplicação Olá
1. Executar `npm install` um terminal tooinstall necessário módulos npm

2. Executar `node app.js` num terminal toostart a aplicação de nó.

Agora pode voltar atrás tooData Explorador e ver a consulta, modificar e trabalhar com estes novos dados. 

## <a name="review-slas-in-hello-azure-portal"></a>Reveja os SLAs no Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:

1. No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Este guia de introdução, aprendeu como toocreate uma conta de base de dados do Azure Cosmos, criar uma coleção utilizando Olá Explorador de dados e executar uma aplicação. Agora pode importar a conta de base de dados do Cosmos tooyour de dados adicionais. 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB](import-data.md) (Importar dados para o Azure Cosmos DB).


