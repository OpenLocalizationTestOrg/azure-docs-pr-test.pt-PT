---
title: "aaaBuild uma aplicação Node.js do Azure Cosmos BD utilizando a Graph API | Microsoft Docs"
description: "Apresenta um exemplo de código Node.js, pode utilizar tooconnect tooand consultar base de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Criar uma aplicação Node.js com o Graph API

BD do Azure do Cosmos é serviço de base de dados com múltiplos modelo Olá globalmente distribuída da Microsoft. Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente. 

Este artigo de início rápido demonstra como toocreate uma base de dados do Azure Cosmos conta Graph API (pré-visualização), a base de dados e o gráfico utilizando Olá portal do Azure. Em seguida, criar e executar uma aplicação de consola utilizando Olá open source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) controlador.  

> [!NOTE]
> módulo de npm Olá `gremlin-secure` é uma versão modificada do `gremlin` módulo, com suporte para SSL e SASL necessárias para ligar a base de dados do Azure Cosmos. O código de origem está disponível no [GitHub](https://github.com/CosmosDB/gremlin-javascript).
>

## <a name="prerequisites"></a>Pré-requisitos

Antes de poder executar este exemplo, tem de ter Olá os seguintes pré-requisitos:
* Versão de [Node.js](https://nodejs.org/en/) v0.10.29 ou superior
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de base de dados

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Adicionar um gráfico

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Aplicação de exemplo de Olá do clone

Agora vamos clone uma Graph API aplicação a partir do GitHub, definir a cadeia de ligação de Olá e executá-la. Verá como é fácil toowork com dados através de programação. 

1. Abra uma janela de terminal do Git, tais como o Git Bash e altere (através de `cd` comando) tooa diretório de trabalho.  

2. Execute Olá repositório do comando tooclone Olá exemplo a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Abra o ficheiro de solução Olá no Visual Studio. 

## <a name="review-hello-code"></a>Rever o código de Olá

Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá. Abra Olá `app.js` ficheiro e, irá encontrar Olá seguintes linhas de código. 

* cliente de Gremlin Olá é criado.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Olá configurações estão todos em `config.js`, que iremos editar no Olá secção a seguir.

* Uma série de passos Gremlin são executados com Olá `client.execute` método.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Atualizar a cadeia de ligação

1. Ficheiro de config.js Olá aberta. 

2. No config.js, preencha a chave de Endpoint Olá com Olá **Gremlin URI** valor Olá **descrição geral** página do Olá portal do Azure. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Ver e copiar uma chave de acesso no Olá portal do Azure, o painel chaves](./media/create-graph-nodejs/gremlin-uri.png)

   Se hello **Gremlin URI** valor está em branco, pode gerar o valor de Olá de Olá **chaves** página no portal de Olá, utilizando Olá **URI** valor, removendo https:// e alteração toographs de documentos.

   ponto final de Gremlin Olá tem de ser único nome de anfitrião de Olá sem número de porta de protocolo/Olá, como `mygraphdb.graphs.azure.com` (não `https://mygraphdb.graphs.azure.com` ou `mygraphdb.graphs.azure.com:433`).

3. Preencha, config.js, valor de config.primaryKey Olá com Olá **chave primária** valor Olá **chaves** página do Olá portal do Azure. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Olá painel de chaves de portal do Azure](./media/create-graph-nodejs/keys.png)

4. Introduza o nome de base de dados de Olá e o nome do gráfico (contentor) para o valor de Olá do config.database e config.collection. 

Eis um exemplo de como deve ser o aspeto do seu ficheiro config.js concluído:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Executar a aplicação de consola Olá

1. Abra uma janela de terminal e altere (através de `cd` comando) toohello o diretório de instalação para o ficheiro de Package. JSON Olá que está incluído no projeto Olá.  

2. Executar `npm install` tooinstall Olá necessário módulos npm, incluindo `gremlin-secure`.

3. Executar `node app.js` num terminal toostart a aplicação de nó.

## <a name="browse-with-data-explorer"></a>Procurar com o Data Explorer

Agora pode voltar atrás tooData Explorer no Olá tooview portal do Azure, consultar, modificar e trabalhar com os novos dados de gráfico.

No Explorador de dados, a nova base de dados Olá aparece no Olá **gráficos** painel. Expanda a base de dados de Olá, seguido de coleção de Olá, em seguida, clique em **gráfico**.

dados de Olá gerados pela aplicação de exemplo de Olá são apresentados no painel seguinte da Olá dentro Olá **gráfico** separador quando clicar em **aplicar filtro**.

Experimente concluir `g.V()` com `.has('firstName', 'Thomas')` filtro de Olá tootest. Tenha em atenção que o valor de Olá é sensível às maiúsculas e minúsculas.

## <a name="review-slas-in-hello-azure-portal"></a>Reveja os SLAs no Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Apague os seus recursos

Se não planear toocontinue utilizar esta aplicação, elimine todos os recursos que criou neste artigo, Olá seguinte: 

1. No Olá portal do Azure, no menu de navegação esquerdo Olá, clique em **grupos de recursos**e, em seguida, clique em nome de Olá do recurso de Olá que criou. 
2. Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome Olá Olá recursos toobe eliminado e, em seguida, clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Neste artigo, aprendeu como criar um gráfico com o Explorador de dados toocreate uma conta de base de dados do Azure Cosmos e executar uma aplicação. Agora pode criar consultas mais complexas e implementar a lógica de passagem de gráfico através do Gremlin. 

> [!div class="nextstepaction"]
> [Query using Gremlin](tutorial-query-graph.md) (Utilizar Gremlin para consultar)
