---
title: "tutorial de aaaNode.js para Olá API do DocumentDB para a base de dados do Azure Cosmos | Microsoft Docs"
description: "Um tutorial de Node.js que cria uma base de dados do Cosmos com Olá API do DocumentDB."
keywords: tutorial de node.js, base de dados de node
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Tutorial de node.js: Olá de utilização DocumentDB API na base de dados do Azure Cosmos toocreate uma aplicação de consola do Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bem-vindo toohello tutorial de Node.js para Olá SDK Node.js do Azure Cosmos DB! Depois de seguir este tutorial, terá de uma aplicação de consola que cria e consulta recursos do Cosmos DB.

Iremos abranger:

* Criar e ligar-se a conta de base de dados do Azure Cosmos tooan
* Configurar a sua aplicação
* Criar uma base de dados Node
* Criação de uma coleção
* Criação de documentos JSON
* Consulta de coleção de Olá
* Substituir um documento
* Eliminar um documento
* Eliminar Olá nó da base de dados

Não tem tempo? Não se preocupe! solução completa de Olá está disponível no [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Consulte [obter a solução completa de Olá](#GetSolution) para instruções rápidas.

Após concluir o tutorial de Node.js Olá,. Utilize Olá votar botões na parte superior do Olá e inferior desta página toogive-nos comentários. Se desejar que enviemos toocontact diretamente, sentir tooinclude livre endereços de e-mail nos seus comentários.

Agora comecemos!

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Pré-requisitos do tutorial de Node.js Olá
Certifique-se de que tem o seguinte Olá:

* Uma conta ativa do Azure. Se não tiver uma, pode inscrever-se numa [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
    * Em alternativa, pode utilizar Olá [emulador de BD do Azure Cosmos](local-emulator.md) para este tutorial.
* Versão [Node.js](https://nodejs.org/) v0.10.29 ou superior.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passo 1: Criar uma conta do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se já tiver uma conta que pretende toouse, pode avançar diretamente demasiado[configurar a sua aplicação Node.js](#SetupNode). Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua aplicação Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Passo 2: Configurar a sua aplicação Node.js
1. Abra o seu terminal favorito.
2. Localize a pasta de Olá ou o diretório onde pretende que toosave sua aplicação Node.js.
3. Crie dois ficheiros JavaScript vazios com Olá os seguintes comandos:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Instale o módulo de documentdb Olá através do npm. Utilize Olá os seguintes comandos:
   * ```npm install documentdb --save```

Ótimo! Agora que concluiu a configuração, comecemos a escrever certos códigos.

## <a id="Config"></a>Passo 3: Configurar as configurações da sua aplicação
Abra ```config.js``` no seu editor de texto favorito.

Em seguida, copiar e colar Olá fragmento de código abaixo e defina as propriedades ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri do ponto final e a chave primária. Ambas as configurações podem ser encontradas na Olá [portal do Azure](https://portal.azure.com).

![Tutorial node.js - captura de ecrã da Olá portal do Azure, que mostra uma conta de base de dados do Azure Cosmos, com o hub de Active Directory Olá realçado, o botão de chaves de Olá realçado no painel de conta de base de dados do Azure Cosmos Olá e Olá URI, valores chave primária e chave secundária realçados no Olá Painel chaves - base de dados Node][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Copie e cole Olá ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` objeto abaixo onde definir o ```config.endpoint``` e ```config.authKey``` propriedades. Se já tiver dados que pretende toostore na base de dados, pode utilizar da BD do Azure Cosmos [ferramenta de migração de dados](import-data.md) em vez de adicionar definições do documento Olá.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Olá da base de dados, coleção e definições do documento irão funcionar como a base de dados do Azure Cosmos ```database id```, ```collection id```e dados dos documentos.

Por fim, exporte o ```config``` objeto, para poder referenciá-lo dentro de Olá ```app.js``` ficheiro.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Passo 4: Ligar a conta de base de dados do Azure Cosmos tooan
Abra o seu vazio ```app.js``` ficheiro num editor de texto Olá. Copie e cole o código de Olá abaixo tooimport Olá ```documentdb``` módulo e a recém-criado ```config``` módulo.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Copie e cole Olá toouse código de Olá guardado anteriormente ```config.endpoint``` e ```config.primaryKey``` toocreate um novo DocumentClient.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Agora que tem o cliente de base de dados do Azure Cosmos do Olá código tooinitialize Olá, vamos ver ao trabalhar com recursos do Azure Cosmos DB.

## <a name="step-5-create-a-node-database"></a>Passo 5: Criar uma base de dados Node
Copie e cole o código de Olá abaixo tooset Olá estado de HTTP para não foi encontrado, o url de base de dados de Olá e o url de coleção Olá. Estes urls são como cliente de base de dados do Azure Cosmos Olá irá encontrar a base de dados à direita do Olá e coleção.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [base de dados](documentdb-resources.md#databases) podem ser criados utilizando Olá [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe. Uma base de dados é o contentor lógico do Olá do armazenamento de documentos particionado em coleções.

Copie e cole Olá **getDatabase** para criar a sua nova base de dados no ficheiro de app.js Olá com Olá ```id``` especificado no Olá ```config``` objeto. Olá função irá verificar se Olá da base de dados com Olá mesmo ```FamilyRegistry``` id já existe. Se existir, iremos devolver essa base de dados em vez de criar uma nova.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copie e cole o código de Olá abaixo onde definir Olá **getDatabase** funcionar a função de programa auxiliar de Olá tooadd **sair** que irá imprimir mensagem de saída de saudação e chamada de Olá demasiado**getDatabase** função.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Criou uma base de dados do Azure Cosmos DB com êxito.

## <a id="CreateColl"></a>Passo 6: Criar uma coleção
> [!WARNING]
> **CreateDocumentCollectionAsync** irá criar uma nova coleção, tendo repercussões sobre os preços. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [coleção](documentdb-resources.md#collections) podem ser criados utilizando Olá [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe. Uma coleção é um contentor de documentos JSON e a lógica da aplicação associada JavaScript.

Copie e cole Olá **getCollection** função, por baixo Olá **getDatabase** funcionar Olá app.js ficheiro toocreate sua nova coleção com Olá ```id``` especificado no Olá ```config```objeto. Novamente, irá verificamos toomake Certifique-se uma coleção com Olá mesmo ```FamilyCollection``` id já existe. Se existir, iremos devolver essa coleção em vez de criar uma nova.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copie e cole o código de Olá abaixo chamada Olá demasiado**getDatabase** tooexecute Olá **getCollection** função.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Uma coleção de base de dados do Azure Cosmos foi criada com êxito.

## <a id="CreateDoc"></a>Passo 7: Criar um documento
A [documento](documentdb-resources.md#documents) podem ser criados utilizando Olá [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe. Os documentos são conteúdos (arbitrários) JSON definidos pelo utilizador. Pode agora inserir um documento no Azure Cosmos DB.

Copie e cole Olá **getFamilyDocument** função, por baixo Olá **getCollection** para criar documentos Olá que contém os dados JSON Olá guardados no Olá ```config``` objeto. Novamente, irá verificamos toomake Certifique-se um documento com Olá mesmo id já existe.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Copie e cole o código de Olá abaixo chamada Olá demasiado**getCollection** tooexecute Olá **getFamilyDocument** função.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Um documento de base de dados do Azure Cosmos foi criada com êxito.

![NODE.js tutorial nó - diagrama que ilustra Olá relação hierárquica entre conta Olá, base de dados de Olá, coleção Olá e Olá documentos - base de dados](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Passo 8: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB suporta [consultas extensas](documentdb-sql-query.md) de documentos JSON armazenados em cada coleção. Olá código de exemplo seguinte mostra uma consulta que pode ser executado contra documentos Olá na sua coleção.

Copie e cole Olá **queryCollection** função, por baixo Olá **getFamilyDocument** função no ficheiro app.js de Olá. BD do Azure do Cosmos suporta consultas de como o SQL Server, como mostrado abaixo. Para obter mais informações sobre como criar consultas complexas, veja Olá [Query Playground](https://www.documentdb.com/sql/demo) e Olá [documentação sobre consultas](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
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
        });
    };


Olá seguinte diagrama ilustra a forma como consulta de base de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de Olá que criou.

![Base de dados node.js tutorial - diagrama que ilustra o âmbito de Olá e o significado da consulta de Olá - Node](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional na consulta de Olá porque as consultas de base de dados do Azure Cosmos já estão confinadas tooa única coleção. Por conseguinte, "FROM Families f" pode ser trocada por "FROM root r" ou qualquer outra variável de nome escolher. BD do Azure do Cosmos irá inferir que famílias, raiz ou o nome da variável Olá escolheu, referência Olá atual coleção por predefinição.

Copie e cole o código de Olá abaixo chamada Olá demasiado**getFamilyDocument** tooexecute Olá **queryCollection** função.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Consultou documentos do Azure Cosmos DB com êxito.

## <a id="ReplaceDocument"></a>Passo 9: Substituir um documento
O Azure Cosmos DB suporta a substituição de documentos JSON.

Copie e cole Olá **replaceFamilyDocument** função, por baixo Olá **queryCollection** função no ficheiro app.js de Olá.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copie e cole o código de Olá abaixo chamada Olá demasiado**queryCollection** tooexecute Olá **replaceDocument** função. Além disso, adicionar Olá código toocall **queryCollection** novamente tooverify esse documento Olá foi alterado com êxito.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Substituiu documentos do Azure Cosmos DB com êxito.

## <a id="DeleteDocument"></a>Passo 10: Eliminar um documento
O Azure Cosmos DB suporta a eliminação de documentos JSON.

Copie e cole Olá **deleteFamilyDocument** função, por baixo Olá **replaceFamilyDocument** função.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copie e cole o código de Olá abaixo Olá chamada toohello segundo **queryCollection** tooexecute Olá **deleteDocument** função.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Parabéns! Eliminou documentos do Azure Cosmos DB com êxito.

## <a id="DeleteDatabase"></a>Passo 11: Eliminar Olá nó da base de dados
A eliminar Olá criada base de dados irá remover a base de dados de Olá e todos os recursos subordinados (coleções, documentos, etc.).

Copie e cole Olá **limpeza** função, por baixo Olá **deleteFamilyDocument** funcionar tooremove Olá da base de dados e todos os recursos subordinados de Olá.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Copie e cole o código de Olá abaixo chamada Olá demasiado**deleteFamilyDocument** tooexecute Olá **limpeza** função.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Passo 12: Executar a sua aplicação Node.js em conjunto!
Completamente, sequência de Olá para chamar as suas funções deve ter o seguinte aspeto:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```

Deverá ver um resultado de Olá da sua aplicação introdução. saída de Olá deve corresponder ao texto de exemplo de Olá abaixo.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Parabéns! Criou concluiu o tutorial de Node.js Olá e ter a sua primeira aplicação de consola de BD do Cosmos Azure!

## <a id="GetSolution"></a>Obter Olá solução completa do Node.js tutorial
Se tive tempo toocomplete Olá passos neste tutorial, ou deseje apenas código de Olá toodownload, pode obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

toorun Olá solução GetStarted que contém todas as amostras de Olá neste artigo, irá necessitar de seguinte Olá:

* [Conta do Azure Cosmos DB][create-account].
* Olá [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solução disponível no GitHub.

Instalar Olá **documentdb** módulo através do npm. Utilize Olá os seguintes comandos:

* ```npm install documentdb --save```

Em seguida, no Olá ```config.js``` de ficheiros, atualização Olá Endpoint e config.authKey valores conforme descrito em [passo 3: definir configurações da sua aplicação](#Config). 

Em seguida, no seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá: ```node app.js```.

Já está, basta criar e está pronto! 

## <a name="next-steps"></a>Passos seguintes
* Pretende um exemplo de Node.js mais complexo? Consulte [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md) (Criar uma aplicação Web Node.js com o Azure Cosmos DB).
* Saiba como demasiado[monitorizar uma conta de base de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas no nosso conjunto de dados de exemplo no Olá [Query Playground](https://www.documentdb.com/sql/demo).
* Saiba mais sobre o modelo de programação Olá no Olá secção desenvolver da Olá [página de documentação do Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
