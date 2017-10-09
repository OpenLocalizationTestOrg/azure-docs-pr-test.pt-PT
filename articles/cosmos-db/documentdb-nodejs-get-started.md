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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="a8f41-104">Tutorial de node.js: Olá de utilização DocumentDB API na base de dados do Azure Cosmos toocreate uma aplicação de consola do Node.js</span><span class="sxs-lookup"><span data-stu-id="a8f41-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8f41-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a8f41-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="a8f41-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a8f41-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="a8f41-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="a8f41-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="a8f41-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8f41-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="a8f41-109">Java</span><span class="sxs-lookup"><span data-stu-id="a8f41-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="a8f41-110">C++</span><span class="sxs-lookup"><span data-stu-id="a8f41-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="a8f41-111">Bem-vindo toohello tutorial de Node.js para Olá SDK Node.js do Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="a8f41-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="a8f41-112">Depois de seguir este tutorial, terá de uma aplicação de consola que cria e consulta recursos do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8f41-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="a8f41-113">Iremos abranger:</span><span class="sxs-lookup"><span data-stu-id="a8f41-113">We'll cover:</span></span>

* <span data-ttu-id="a8f41-114">Criar e ligar-se a conta de base de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="a8f41-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="a8f41-115">Configurar a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="a8f41-115">Setting up your application</span></span>
* <span data-ttu-id="a8f41-116">Criar uma base de dados Node</span><span class="sxs-lookup"><span data-stu-id="a8f41-116">Creating a node database</span></span>
* <span data-ttu-id="a8f41-117">Criação de uma coleção</span><span class="sxs-lookup"><span data-stu-id="a8f41-117">Creating a collection</span></span>
* <span data-ttu-id="a8f41-118">Criação de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="a8f41-118">Creating JSON documents</span></span>
* <span data-ttu-id="a8f41-119">Consulta de coleção de Olá</span><span class="sxs-lookup"><span data-stu-id="a8f41-119">Querying hello collection</span></span>
* <span data-ttu-id="a8f41-120">Substituir um documento</span><span class="sxs-lookup"><span data-stu-id="a8f41-120">Replacing a document</span></span>
* <span data-ttu-id="a8f41-121">Eliminar um documento</span><span class="sxs-lookup"><span data-stu-id="a8f41-121">Deleting a document</span></span>
* <span data-ttu-id="a8f41-122">Eliminar Olá nó da base de dados</span><span class="sxs-lookup"><span data-stu-id="a8f41-122">Deleting hello node database</span></span>

<span data-ttu-id="a8f41-123">Não tem tempo?</span><span class="sxs-lookup"><span data-stu-id="a8f41-123">Don't have time?</span></span> <span data-ttu-id="a8f41-124">Não se preocupe!</span><span class="sxs-lookup"><span data-stu-id="a8f41-124">Don't worry!</span></span> <span data-ttu-id="a8f41-125">solução completa de Olá está disponível no [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a8f41-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="a8f41-126">Consulte [obter a solução completa de Olá](#GetSolution) para instruções rápidas.</span><span class="sxs-lookup"><span data-stu-id="a8f41-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="a8f41-127">Após concluir o tutorial de Node.js Olá,. Utilize Olá votar botões na parte superior do Olá e inferior desta página toogive-nos comentários.</span><span class="sxs-lookup"><span data-stu-id="a8f41-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="a8f41-128">Se desejar que enviemos toocontact diretamente, sentir tooinclude livre endereços de e-mail nos seus comentários.</span><span class="sxs-lookup"><span data-stu-id="a8f41-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="a8f41-129">Agora comecemos!</span><span class="sxs-lookup"><span data-stu-id="a8f41-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="a8f41-130">Pré-requisitos do tutorial de Node.js Olá</span><span class="sxs-lookup"><span data-stu-id="a8f41-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="a8f41-131">Certifique-se de que tem o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a8f41-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="a8f41-132">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8f41-132">An active Azure account.</span></span> <span data-ttu-id="a8f41-133">Se não tiver uma, pode inscrever-se numa [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8f41-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="a8f41-134">Em alternativa, pode utilizar Olá [emulador de BD do Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8f41-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="a8f41-135">Versão [Node.js](https://nodejs.org/) v0.10.29 ou superior.</span><span class="sxs-lookup"><span data-stu-id="a8f41-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="a8f41-136">Passo 1: Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a8f41-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="a8f41-137">Vamos criar uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8f41-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="a8f41-138">Se já tiver uma conta que pretende toouse, pode avançar diretamente demasiado[configurar a sua aplicação Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="a8f41-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="a8f41-139">Se estiver a utilizar Olá emulador de BD do Cosmos do Azure, siga os passos de Olá em [emulador de BD do Azure Cosmos](local-emulator.md) toosetup Olá emulador e avançar diretamente demasiado[configurar a sua aplicação Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="a8f41-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a8f41-140"><a id="SetupNode"></a>Passo 2: Configurar a sua aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="a8f41-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="a8f41-141">Abra o seu terminal favorito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="a8f41-142">Localize a pasta de Olá ou o diretório onde pretende que toosave sua aplicação Node.js.</span><span class="sxs-lookup"><span data-stu-id="a8f41-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="a8f41-143">Crie dois ficheiros JavaScript vazios com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8f41-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="a8f41-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="a8f41-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="a8f41-145">Linux/OS X:</span><span class="sxs-lookup"><span data-stu-id="a8f41-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="a8f41-146">Instale o módulo de documentdb Olá através do npm.</span><span class="sxs-lookup"><span data-stu-id="a8f41-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="a8f41-147">Utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8f41-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="a8f41-148">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="a8f41-148">Great!</span></span> <span data-ttu-id="a8f41-149">Agora que concluiu a configuração, comecemos a escrever certos códigos.</span><span class="sxs-lookup"><span data-stu-id="a8f41-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="a8f41-150"><a id="Config"></a>Passo 3: Configurar as configurações da sua aplicação</span><span class="sxs-lookup"><span data-stu-id="a8f41-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="a8f41-151">Abra ```config.js``` no seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="a8f41-152">Em seguida, copiar e colar Olá fragmento de código abaixo e defina as propriedades ```config.endpoint``` e ```config.primaryKey``` tooyour Azure Cosmos DB uri do ponto final e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="a8f41-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="a8f41-153">Ambas as configurações podem ser encontradas na Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8f41-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Tutorial node.js - captura de ecrã da Olá portal do Azure, que mostra uma conta de base de dados do Azure Cosmos, com o hub de Active Directory Olá realçado, o botão de chaves de Olá realçado no painel de conta de base de dados do Azure Cosmos Olá e Olá URI, valores chave primária e chave secundária realçados no Olá Painel chaves - base de dados Node][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="a8f41-155">Copie e cole Olá ```database id```, ```collection id```, e ```JSON documents``` tooyour ```config``` objeto abaixo onde definir o ```config.endpoint``` e ```config.authKey``` propriedades.</span><span class="sxs-lookup"><span data-stu-id="a8f41-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="a8f41-156">Se já tiver dados que pretende toostore na base de dados, pode utilizar da BD do Azure Cosmos [ferramenta de migração de dados](import-data.md) em vez de adicionar definições do documento Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

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


<span data-ttu-id="a8f41-157">Olá da base de dados, coleção e definições do documento irão funcionar como a base de dados do Azure Cosmos ```database id```, ```collection id```e dados dos documentos.</span><span class="sxs-lookup"><span data-stu-id="a8f41-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="a8f41-158">Por fim, exporte o ```config``` objeto, para poder referenciá-lo dentro de Olá ```app.js``` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a8f41-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="a8f41-159"><a id="Connect"></a>Passo 4: Ligar a conta de base de dados do Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="a8f41-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="a8f41-160">Abra o seu vazio ```app.js``` ficheiro num editor de texto Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="a8f41-161">Copie e cole o código de Olá abaixo tooimport Olá ```documentdb``` módulo e a recém-criado ```config``` módulo.</span><span class="sxs-lookup"><span data-stu-id="a8f41-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="a8f41-162">Copie e cole Olá toouse código de Olá guardado anteriormente ```config.endpoint``` e ```config.primaryKey``` toocreate um novo DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="a8f41-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="a8f41-163">Agora que tem o cliente de base de dados do Azure Cosmos do Olá código tooinitialize Olá, vamos ver ao trabalhar com recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8f41-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="a8f41-164">Passo 5: Criar uma base de dados Node</span><span class="sxs-lookup"><span data-stu-id="a8f41-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="a8f41-165">Copie e cole o código de Olá abaixo tooset Olá estado de HTTP para não foi encontrado, o url de base de dados de Olá e o url de coleção Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="a8f41-166">Estes urls são como cliente de base de dados do Azure Cosmos Olá irá encontrar a base de dados à direita do Olá e coleção.</span><span class="sxs-lookup"><span data-stu-id="a8f41-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="a8f41-167">A [base de dados](documentdb-resources.md#databases) podem ser criados utilizando Olá [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a8f41-168">Uma base de dados é o contentor lógico do Olá do armazenamento de documentos particionado em coleções.</span><span class="sxs-lookup"><span data-stu-id="a8f41-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="a8f41-169">Copie e cole Olá **getDatabase** para criar a sua nova base de dados no ficheiro de app.js Olá com Olá ```id``` especificado no Olá ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="a8f41-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="a8f41-170">Olá função irá verificar se Olá da base de dados com Olá mesmo ```FamilyRegistry``` id já existe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="a8f41-171">Se existir, iremos devolver essa base de dados em vez de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="a8f41-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

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

<span data-ttu-id="a8f41-172">Copie e cole o código de Olá abaixo onde definir Olá **getDatabase** funcionar a função de programa auxiliar de Olá tooadd **sair** que irá imprimir mensagem de saída de saudação e chamada de Olá demasiado**getDatabase** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

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

<span data-ttu-id="a8f41-173">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-174">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-174">Congratulations!</span></span> <span data-ttu-id="a8f41-175">Criou uma base de dados do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="a8f41-176"><a id="CreateColl"></a>Passo 6: Criar uma coleção</span><span class="sxs-lookup"><span data-stu-id="a8f41-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="a8f41-177">**CreateDocumentCollectionAsync** irá criar uma nova coleção, tendo repercussões sobre os preços.</span><span class="sxs-lookup"><span data-stu-id="a8f41-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="a8f41-178">Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="a8f41-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="a8f41-179">A [coleção](documentdb-resources.md#collections) podem ser criados utilizando Olá [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a8f41-180">Uma coleção é um contentor de documentos JSON e a lógica da aplicação associada JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a8f41-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="a8f41-181">Copie e cole Olá **getCollection** função, por baixo Olá **getDatabase** funcionar Olá app.js ficheiro toocreate sua nova coleção com Olá ```id``` especificado no Olá ```config```objeto.</span><span class="sxs-lookup"><span data-stu-id="a8f41-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="a8f41-182">Novamente, irá verificamos toomake Certifique-se uma coleção com Olá mesmo ```FamilyCollection``` id já existe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="a8f41-183">Se existir, iremos devolver essa coleção em vez de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="a8f41-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

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

<span data-ttu-id="a8f41-184">Copie e cole o código de Olá abaixo chamada Olá demasiado**getDatabase** tooexecute Olá **getCollection** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a8f41-185">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-186">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-186">Congratulations!</span></span> <span data-ttu-id="a8f41-187">Uma coleção de base de dados do Azure Cosmos foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="a8f41-188"><a id="CreateDoc"></a>Passo 7: Criar um documento</span><span class="sxs-lookup"><span data-stu-id="a8f41-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="a8f41-189">A [documento](documentdb-resources.md#documents) podem ser criados utilizando Olá [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) função de Olá **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="a8f41-190">Os documentos são conteúdos (arbitrários) JSON definidos pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="a8f41-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a8f41-191">Pode agora inserir um documento no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8f41-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="a8f41-192">Copie e cole Olá **getFamilyDocument** função, por baixo Olá **getCollection** para criar documentos Olá que contém os dados JSON Olá guardados no Olá ```config``` objeto.</span><span class="sxs-lookup"><span data-stu-id="a8f41-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="a8f41-193">Novamente, irá verificamos toomake Certifique-se um documento com Olá mesmo id já existe.</span><span class="sxs-lookup"><span data-stu-id="a8f41-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

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

<span data-ttu-id="a8f41-194">Copie e cole o código de Olá abaixo chamada Olá demasiado**getCollection** tooexecute Olá **getFamilyDocument** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a8f41-195">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-196">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-196">Congratulations!</span></span> <span data-ttu-id="a8f41-197">Um documento de base de dados do Azure Cosmos foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-197">You have successfully created an Azure Cosmos DB document.</span></span>

![NODE.js tutorial nó - diagrama que ilustra Olá relação hierárquica entre conta Olá, base de dados de Olá, coleção Olá e Olá documentos - base de dados](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="a8f41-199"><a id="Query"></a>Passo 8: Consultar recursos do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a8f41-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="a8f41-200">O Azure Cosmos DB suporta [consultas extensas](documentdb-sql-query.md) de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="a8f41-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="a8f41-201">Olá código de exemplo seguinte mostra uma consulta que pode ser executado contra documentos Olá na sua coleção.</span><span class="sxs-lookup"><span data-stu-id="a8f41-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="a8f41-202">Copie e cole Olá **queryCollection** função, por baixo Olá **getFamilyDocument** função no ficheiro app.js de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="a8f41-203">BD do Azure do Cosmos suporta consultas de como o SQL Server, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8f41-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="a8f41-204">Para obter mais informações sobre como criar consultas complexas, veja Olá [Query Playground](https://www.documentdb.com/sql/demo) e Olá [documentação sobre consultas](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="a8f41-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

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


<span data-ttu-id="a8f41-205">Olá seguinte diagrama ilustra a forma como consulta de base de dados SQL do Azure Cosmos Olá sintaxe é chamada na coleção de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="a8f41-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Base de dados node.js tutorial - diagrama que ilustra o âmbito de Olá e o significado da consulta de Olá - Node](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="a8f41-207">Olá [FROM](documentdb-sql-query.md#FromClause) palavra-chave é opcional na consulta de Olá porque as consultas de base de dados do Azure Cosmos já estão confinadas tooa única coleção.</span><span class="sxs-lookup"><span data-stu-id="a8f41-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="a8f41-208">Por conseguinte, "FROM Families f" pode ser trocada por "FROM root r" ou qualquer outra variável de nome escolher.</span><span class="sxs-lookup"><span data-stu-id="a8f41-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="a8f41-209">BD do Azure do Cosmos irá inferir que famílias, raiz ou o nome da variável Olá escolheu, referência Olá atual coleção por predefinição.</span><span class="sxs-lookup"><span data-stu-id="a8f41-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="a8f41-210">Copie e cole o código de Olá abaixo chamada Olá demasiado**getFamilyDocument** tooexecute Olá **queryCollection** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a8f41-211">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-212">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-212">Congratulations!</span></span> <span data-ttu-id="a8f41-213">Consultou documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="a8f41-214"><a id="ReplaceDocument"></a>Passo 9: Substituir um documento</span><span class="sxs-lookup"><span data-stu-id="a8f41-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="a8f41-215">O Azure Cosmos DB suporta a substituição de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="a8f41-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="a8f41-216">Copie e cole Olá **replaceFamilyDocument** função, por baixo Olá **queryCollection** função no ficheiro app.js de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

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

<span data-ttu-id="a8f41-217">Copie e cole o código de Olá abaixo chamada Olá demasiado**queryCollection** tooexecute Olá **replaceDocument** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="a8f41-218">Além disso, adicionar Olá código toocall **queryCollection** novamente tooverify esse documento Olá foi alterado com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a8f41-219">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-220">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-220">Congratulations!</span></span> <span data-ttu-id="a8f41-221">Substituiu documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a8f41-222"><a id="DeleteDocument"></a>Passo 10: Eliminar um documento</span><span class="sxs-lookup"><span data-stu-id="a8f41-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="a8f41-223">O Azure Cosmos DB suporta a eliminação de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="a8f41-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="a8f41-224">Copie e cole Olá **deleteFamilyDocument** função, por baixo Olá **replaceFamilyDocument** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

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

<span data-ttu-id="a8f41-225">Copie e cole o código de Olá abaixo Olá chamada toohello segundo **queryCollection** tooexecute Olá **deleteDocument** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="a8f41-226">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-227">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-227">Congratulations!</span></span> <span data-ttu-id="a8f41-228">Eliminou documentos do Azure Cosmos DB com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8f41-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a8f41-229"><a id="DeleteDatabase"></a>Passo 11: Eliminar Olá nó da base de dados</span><span class="sxs-lookup"><span data-stu-id="a8f41-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="a8f41-230">A eliminar Olá criada base de dados irá remover a base de dados de Olá e todos os recursos subordinados (coleções, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="a8f41-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="a8f41-231">Copie e cole Olá **limpeza** função, por baixo Olá **deleteFamilyDocument** funcionar tooremove Olá da base de dados e todos os recursos subordinados de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8f41-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

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

<span data-ttu-id="a8f41-232">Copie e cole o código de Olá abaixo chamada Olá demasiado**deleteFamilyDocument** tooexecute Olá **limpeza** função.</span><span class="sxs-lookup"><span data-stu-id="a8f41-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="a8f41-233"><a id="Run"></a>Passo 12: Executar a sua aplicação Node.js em conjunto!</span><span class="sxs-lookup"><span data-stu-id="a8f41-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="a8f41-234">Completamente, sequência de Olá para chamar as suas funções deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="a8f41-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="a8f41-235">No seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="a8f41-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="a8f41-236">Deverá ver um resultado de Olá da sua aplicação introdução.</span><span class="sxs-lookup"><span data-stu-id="a8f41-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="a8f41-237">saída de Olá deve corresponder ao texto de exemplo de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="a8f41-237">hello output should match hello example text below.</span></span>

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

<span data-ttu-id="a8f41-238">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a8f41-238">Congratulations!</span></span> <span data-ttu-id="a8f41-239">Criou concluiu o tutorial de Node.js Olá e ter a sua primeira aplicação de consola de BD do Cosmos Azure!</span><span class="sxs-lookup"><span data-stu-id="a8f41-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="a8f41-240"><a id="GetSolution"></a>Obter Olá solução completa do Node.js tutorial</span><span class="sxs-lookup"><span data-stu-id="a8f41-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="a8f41-241">Se tive tempo toocomplete Olá passos neste tutorial, ou deseje apenas código de Olá toodownload, pode obtê-lo de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a8f41-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="a8f41-242">toorun Olá solução GetStarted que contém todas as amostras de Olá neste artigo, irá necessitar de seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a8f41-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="a8f41-243">[Conta do Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="a8f41-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="a8f41-244">Olá [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solução disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8f41-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="a8f41-245">Instalar Olá **documentdb** módulo através do npm.</span><span class="sxs-lookup"><span data-stu-id="a8f41-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="a8f41-246">Utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a8f41-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="a8f41-247">Em seguida, no Olá ```config.js``` de ficheiros, atualização Olá Endpoint e config.authKey valores conforme descrito em [passo 3: definir configurações da sua aplicação](#Config).</span><span class="sxs-lookup"><span data-stu-id="a8f41-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="a8f41-248">Em seguida, no seu terminal, localize o ```app.js``` do ficheiro e execute o comando de Olá: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="a8f41-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="a8f41-249">Já está, basta criar e está pronto!</span><span class="sxs-lookup"><span data-stu-id="a8f41-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a8f41-250">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a8f41-250">Next steps</span></span>
* <span data-ttu-id="a8f41-251">Pretende um exemplo de Node.js mais complexo?</span><span class="sxs-lookup"><span data-stu-id="a8f41-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="a8f41-252">Consulte [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md) (Criar uma aplicação Web Node.js com o Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="a8f41-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="a8f41-253">Saiba como demasiado[monitorizar uma conta de base de dados do Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a8f41-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="a8f41-254">Executar consultas no nosso conjunto de dados de exemplo no Olá [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="a8f41-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a8f41-255">Saiba mais sobre o modelo de programação Olá no Olá secção desenvolver da Olá [página de documentação do Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a8f41-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
