---
title: "aaaCreate uma base de dados de gráfico de BD do Cosmos do Azure com o Java | Microsoft Docs"
description: "Apresenta uma Java o código de exemplo, pode utilizar dados de gráfico tooconnect tooand consulta na base de dados do Cosmos Azure Gremlin a utilizar."
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
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="41dc0-103">BD do Azure do Cosmos: Criar uma base de dados do gráfico com o Java e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41dc0-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="41dc0-104">O Azure Cosmos DB é um serviço de bases de dados com vários modelos e distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41dc0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="41dc0-105">Pode criar e consultar documentos, chave/valor e bases de dados de gráfico, sendo todas beneficiam das capacidades de dimensionamento horizontal núcleo Olá da base de dados do Azure Cosmos e distribuição global Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="41dc0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="41dc0-106">Este guia de introdução cria um gráfico da base de dados utilizando Olá ferramentas portais do Azure para a base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="41dc0-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="41dc0-107">Este guia de introdução mostra também como tooquickly criar uma aplicação de consola Java utilizando uma base de dados do gráfico com Olá OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) controlador.</span><span class="sxs-lookup"><span data-stu-id="41dc0-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="41dc0-108">Olá instruções deste guia de introdução podem ser seguidas em qualquer sistema operativo que seja capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="41dc0-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="41dc0-109">Este guia de introdução o familiarizes com criar e modificar recursos do gráfico na Olá IU ou através de programação, optando-se a sua preferência.</span><span class="sxs-lookup"><span data-stu-id="41dc0-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="41dc0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41dc0-110">Prerequisites</span></span>

* [<span data-ttu-id="41dc0-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="41dc0-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="41dc0-112">Ubuntu, executado `apt-get install default-jdk` tooinstall Olá JDK.</span><span class="sxs-lookup"><span data-stu-id="41dc0-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="41dc0-113">Ser tooset se Olá JAVA_HOME ambiente toopoint variável toohello pasta onde Olá JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="41dc0-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="41dc0-114">[Transferir](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um arquivo binário [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="41dc0-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="41dc0-115">No Ubuntu, pode executar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="41dc0-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="41dc0-116">Git</span><span class="sxs-lookup"><span data-stu-id="41dc0-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="41dc0-117">No Ubuntu, pode executar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="41dc0-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="41dc0-118">Criar uma conta de base de dados</span><span class="sxs-lookup"><span data-stu-id="41dc0-118">Create a database account</span></span>

<span data-ttu-id="41dc0-119">Antes de poder criar uma base de dados do gráfico, terá de toocreate uma conta de base de dados Gremlin (gráfico) com base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="41dc0-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="41dc0-120">Adicionar um gráfico</span><span class="sxs-lookup"><span data-stu-id="41dc0-120">Add a graph</span></span>

<span data-ttu-id="41dc0-121">Agora, pode utilizar a ferramenta Explorador de dados de Olá no Olá toocreate do portal do Azure, uma base de dados do gráfico.</span><span class="sxs-lookup"><span data-stu-id="41dc0-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="41dc0-122">No Olá portal do Azure, no menu de navegação esquerdo Olá, clique em **Explorador de dados (pré-visualização)**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="41dc0-123">No Olá **Explorador de dados (pré-visualização)** painel, clique em **gráfico novo**, em seguida, preencha a página Olá utilizando Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="41dc0-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Explorador de dados no Olá portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="41dc0-125">Definição</span><span class="sxs-lookup"><span data-stu-id="41dc0-125">Setting</span></span>|<span data-ttu-id="41dc0-126">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="41dc0-126">Suggested value</span></span>|<span data-ttu-id="41dc0-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="41dc0-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="41dc0-128">ID da base de dados</span><span class="sxs-lookup"><span data-stu-id="41dc0-128">Database ID</span></span>|<span data-ttu-id="41dc0-129">base de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="41dc0-129">sample-database</span></span>|<span data-ttu-id="41dc0-130">Olá ID para a sua nova base de dados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-130">hello ID for your new database.</span></span> <span data-ttu-id="41dc0-131">Os nomes das bases de dados têm de ter entre um e 255 carateres e não podem conter `/ \ # ?` nem espaços à direita.</span><span class="sxs-lookup"><span data-stu-id="41dc0-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="41dc0-132">ID do Graph</span><span class="sxs-lookup"><span data-stu-id="41dc0-132">Graph ID</span></span>|<span data-ttu-id="41dc0-133">gráfico de exemplo</span><span class="sxs-lookup"><span data-stu-id="41dc0-133">sample-graph</span></span>|<span data-ttu-id="41dc0-134">ID de Olá para o novo gráfico.</span><span class="sxs-lookup"><span data-stu-id="41dc0-134">hello ID for your new graph.</span></span> <span data-ttu-id="41dc0-135">Os nomes de gráfico têm Olá requisitos mesmo caráter como ids de base de dados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="41dc0-136">Capacidade de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="41dc0-136">Storage Capacity</span></span>| <span data-ttu-id="41dc0-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="41dc0-137">10 GB</span></span>|<span data-ttu-id="41dc0-138">Deixe o valor predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-138">Leave hello default value.</span></span> <span data-ttu-id="41dc0-139">Esta é a capacidade de armazenamento Olá da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="41dc0-140">Débito</span><span class="sxs-lookup"><span data-stu-id="41dc0-140">Throughput</span></span>|<span data-ttu-id="41dc0-141">400 RUs</span><span class="sxs-lookup"><span data-stu-id="41dc0-141">400 RUs</span></span>|<span data-ttu-id="41dc0-142">Deixe o valor predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-142">Leave hello default value.</span></span> <span data-ttu-id="41dc0-143">Pode dimensionar débito hello mais tarde se quiser tooreduce latência.</span><span class="sxs-lookup"><span data-stu-id="41dc0-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="41dc0-144">Chave de partição</span><span class="sxs-lookup"><span data-stu-id="41dc0-144">Partition key</span></span>|<span data-ttu-id="41dc0-145">Deixar em branco</span><span class="sxs-lookup"><span data-stu-id="41dc0-145">Leave blank</span></span>|<span data-ttu-id="41dc0-146">Para efeitos de Olá deste guia de introdução, deixe a chave de partição Olá em branco.</span><span class="sxs-lookup"><span data-stu-id="41dc0-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="41dc0-147">Depois do formulário de Olá é preenchido, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="41dc0-148">Aplicação de exemplo de Olá do clone</span><span class="sxs-lookup"><span data-stu-id="41dc0-148">Clone hello sample application</span></span>

<span data-ttu-id="41dc0-149">Agora vamos clonar uma aplicação de gráfico a partir do github, definir a cadeia de ligação de Olá e executá-la.</span><span class="sxs-lookup"><span data-stu-id="41dc0-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="41dc0-150">Pode ver como é fácil toowork com dados através de programação.</span><span class="sxs-lookup"><span data-stu-id="41dc0-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="41dc0-151">Abra uma janela de terminal do git, tais como o git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="41dc0-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="41dc0-152">Execute Olá repositório do comando tooclone Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="41dc0-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="41dc0-153">Rever o código de Olá</span><span class="sxs-lookup"><span data-stu-id="41dc0-153">Review hello code</span></span>

<span data-ttu-id="41dc0-154">Certifiquemo-numa revisão rápida do que está a acontecer na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="41dc0-155">Abra Olá `Program.java` ficheiros da pasta de \src\GetStarted Olá e localizar estas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="41dc0-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="41dc0-156">Olá Gremlin `Client` é inicializado da configuração de Olá no `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="41dc0-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="41dc0-157">Uma série de passos Gremlin são executados utilizando Olá `client.submit` método.</span><span class="sxs-lookup"><span data-stu-id="41dc0-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="41dc0-158">Atualizar a cadeia de ligação</span><span class="sxs-lookup"><span data-stu-id="41dc0-158">Update your connection string</span></span>

1. <span data-ttu-id="41dc0-159">Ficheiro de src/remote.yaml Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="41dc0-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="41dc0-160">Preencha o *anfitriões*, *username*, e *palavra-passe* valores no ficheiro de src/remote.yaml Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="41dc0-161">rest Olá das definições de Olá não é necessário toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="41dc0-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="41dc0-162">Definição</span><span class="sxs-lookup"><span data-stu-id="41dc0-162">Setting</span></span>|<span data-ttu-id="41dc0-163">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="41dc0-163">Suggested value</span></span>|<span data-ttu-id="41dc0-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="41dc0-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="41dc0-165">Anfitriões</span><span class="sxs-lookup"><span data-stu-id="41dc0-165">Hosts</span></span>|<span data-ttu-id="41dc0-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="41dc0-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="41dc0-167">Consulte a captura de ecrã de Olá após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="41dc0-167">See hello screenshot following this table.</span></span> <span data-ttu-id="41dc0-168">Este valor é o valor do URI de Gremlin Olá na página de descrição geral de Olá de Olá portal do Azure, entre parênteses Retos, com um Olá: 443 / removido.</span><span class="sxs-lookup"><span data-stu-id="41dc0-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="41dc0-169">Este valor também pode ser obtido a partir do separador de chaves Olá, utilizando o valor do URI Olá ao remover https://, alterar toographs de documentos e remover à direita Olá: 443 /.</span><span class="sxs-lookup"><span data-stu-id="41dc0-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="41dc0-170">Nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="41dc0-170">Username</span></span>|<span data-ttu-id="41dc0-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="41dc0-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="41dc0-172">Olá recursos com formato Olá `/dbs/<db>/colls/<coll>` onde `<db>` é o nome de base de dados existente e `<coll>` é o nome de coleção existente.</span><span class="sxs-lookup"><span data-stu-id="41dc0-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="41dc0-173">Palavra-passe</span><span class="sxs-lookup"><span data-stu-id="41dc0-173">Password</span></span>|<span data-ttu-id="41dc0-174">*A chave mestra principal*</span><span class="sxs-lookup"><span data-stu-id="41dc0-174">*Your primary master key*</span></span>|<span data-ttu-id="41dc0-175">Consulte Olá captura de ecrã segundo após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="41dc0-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="41dc0-176">Este valor é a chave primária, o que pode obter a partir da página de chaves de Olá de Olá portal do Azure, na caixa de chave primária de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="41dc0-177">Copie o valor de Olá utilizando o botão de copiar Olá no lado direito de Olá da caixa de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="41dc0-178">Para o valor de anfitriões de Olá, copie Olá **Gremlin URI** valor Olá **descrição geral** página.</span><span class="sxs-lookup"><span data-stu-id="41dc0-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="41dc0-179">Se estiver vazia, consulte as instruções de Olá na linha de anfitriões de Olá no Olá precedente tabela sobre a criação de Olá Gremlin URI a partir do painel de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="41dc0-180">![Ver e copiar Olá Gremlin o valor URI na página de descrição geral de Olá no Olá portal do Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="41dc0-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="41dc0-181">Para o valor de palavra-passe Olá, copie Olá **chave primária** de Olá **chaves** painel: ![ver e copiar a chave primária no portal do Azure, de Olá chaves página](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="41dc0-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="41dc0-182">Executar a aplicação de consola Olá</span><span class="sxs-lookup"><span data-stu-id="41dc0-182">Run hello console app</span></span>

1. <span data-ttu-id="41dc0-183">Na janela de terminal git Olá, `cd` pasta azure-cosmos-db-graph-java-getting-started toohello.</span><span class="sxs-lookup"><span data-stu-id="41dc0-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="41dc0-184">Na janela de terminal git Olá, escreva `mvn package` tooinstall Olá necessário pacotes de Java.</span><span class="sxs-lookup"><span data-stu-id="41dc0-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="41dc0-185">Na janela de terminal git Olá, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no Olá toostart de janela de terminal, a aplicação de Java.</span><span class="sxs-lookup"><span data-stu-id="41dc0-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="41dc0-186">janela de terminal Olá apresenta vértices Olá a serem adicionados toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="41dc0-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="41dc0-187">Após a conclusão do programa de Olá, mude toohello back portal do Azure no seu browser da internet.</span><span class="sxs-lookup"><span data-stu-id="41dc0-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="41dc0-188">Rever e adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="41dc0-188">Review and add sample data</span></span>

<span data-ttu-id="41dc0-189">Agora pode voltar atrás tooData Explorador e ver vértices Olá adicionados toohello gráfico e adicionar pontos de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="41dc0-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="41dc0-190">No Explorador de dados, expanda Olá **base de dados de exemplo**/**exemplo gráfico**, clique em **gráfico**e, em seguida, clique em **aplicar o filtro**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Criar novos documentos no Explorador de dados no Olá portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="41dc0-192">No Olá **resultados** lista, tenha em atenção de que os novos utilizadores Olá adicionado toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="41dc0-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="41dc0-193">Selecione **Bernardo** e repare que ele estabeleceu toorobin.</span><span class="sxs-lookup"><span data-stu-id="41dc0-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="41dc0-194">Pode mover vértices Olá-se no Explorador do gráfico Olá, ampliar e reduzir e expandir o tamanho de Olá da superfície de Explorador de gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Novo vértices no gráfico de Olá no Explorador de dados no Olá portal do Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="41dc0-196">Vamos adicionar alguns gráfico de toohello de utilizadores novos com Olá Explorador de dados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="41dc0-197">Clique em Olá **vértice novo** gráfico tooyour do botão tooadd dados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Criar novos documentos no Explorador de dados no Olá portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="41dc0-199">Introduza uma etiqueta de *pessoa* , em seguida, introduza Olá seguintes chaves e valores toocreate vértice primeiro de Olá no gráfico de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="41dc0-200">Tenha em atenção que pode criar propriedades exclusivas para cada pessoa no seu gráfico.</span><span class="sxs-lookup"><span data-stu-id="41dc0-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="41dc0-201">Chave de id de Olá só é necessária.</span><span class="sxs-lookup"><span data-stu-id="41dc0-201">Only hello id key is required.</span></span>

    <span data-ttu-id="41dc0-202">key</span><span class="sxs-lookup"><span data-stu-id="41dc0-202">key</span></span>|<span data-ttu-id="41dc0-203">valor</span><span class="sxs-lookup"><span data-stu-id="41dc0-203">value</span></span>|<span data-ttu-id="41dc0-204">Notas</span><span class="sxs-lookup"><span data-stu-id="41dc0-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="41dc0-205">ID</span><span class="sxs-lookup"><span data-stu-id="41dc0-205">id</span></span>|<span data-ttu-id="41dc0-206">ashley</span><span class="sxs-lookup"><span data-stu-id="41dc0-206">ashley</span></span>|<span data-ttu-id="41dc0-207">Olá Identificador exclusivo para o vértice Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="41dc0-208">Se não especificar, é gerado um id automaticamente.</span><span class="sxs-lookup"><span data-stu-id="41dc0-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="41dc0-209">género</span><span class="sxs-lookup"><span data-stu-id="41dc0-209">gender</span></span>|<span data-ttu-id="41dc0-210">feminino</span><span class="sxs-lookup"><span data-stu-id="41dc0-210">female</span></span>| 
    <span data-ttu-id="41dc0-211">técnico</span><span class="sxs-lookup"><span data-stu-id="41dc0-211">tech</span></span> | <span data-ttu-id="41dc0-212">java</span><span class="sxs-lookup"><span data-stu-id="41dc0-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="41dc0-213">Neste guia de início rápido, criámos uma coleção não particionada.</span><span class="sxs-lookup"><span data-stu-id="41dc0-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="41dc0-214">No entanto, se criar uma coleção particionada ao especificar uma chave de partição durante a criação de coleção de Olá, terá de chave de partição de Olá tooinclude como uma chave em cada novo vértice.</span><span class="sxs-lookup"><span data-stu-id="41dc0-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="41dc0-215">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-215">Click **OK**.</span></span> <span data-ttu-id="41dc0-216">Poderá ser necessário tooexpand toosee o ecrã **OK** no Olá parte inferior do ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="41dc0-217">Clique em **Vértice Novo** novamente e adicione outro utilizador.</span><span class="sxs-lookup"><span data-stu-id="41dc0-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="41dc0-218">Introduza uma etiqueta de *pessoa* , em seguida, introduza o seguinte Olá chaves e valores:</span><span class="sxs-lookup"><span data-stu-id="41dc0-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="41dc0-219">key</span><span class="sxs-lookup"><span data-stu-id="41dc0-219">key</span></span>|<span data-ttu-id="41dc0-220">valor</span><span class="sxs-lookup"><span data-stu-id="41dc0-220">value</span></span>|<span data-ttu-id="41dc0-221">Notas</span><span class="sxs-lookup"><span data-stu-id="41dc0-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="41dc0-222">ID</span><span class="sxs-lookup"><span data-stu-id="41dc0-222">id</span></span>|<span data-ttu-id="41dc0-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="41dc0-223">rakesh</span></span>|<span data-ttu-id="41dc0-224">Olá Identificador exclusivo para o vértice Olá.</span><span class="sxs-lookup"><span data-stu-id="41dc0-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="41dc0-225">Se não especificar, é gerado um id automaticamente.</span><span class="sxs-lookup"><span data-stu-id="41dc0-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="41dc0-226">género</span><span class="sxs-lookup"><span data-stu-id="41dc0-226">gender</span></span>|<span data-ttu-id="41dc0-227">masculino</span><span class="sxs-lookup"><span data-stu-id="41dc0-227">male</span></span>| 
    <span data-ttu-id="41dc0-228">escola</span><span class="sxs-lookup"><span data-stu-id="41dc0-228">school</span></span>|<span data-ttu-id="41dc0-229">MIT</span><span class="sxs-lookup"><span data-stu-id="41dc0-229">MIT</span></span>| 

7. <span data-ttu-id="41dc0-230">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-230">Click **OK**.</span></span> 

8. <span data-ttu-id="41dc0-231">Clique em **aplicar filtro** com predefinição Olá `g.V()` filtro.</span><span class="sxs-lookup"><span data-stu-id="41dc0-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="41dc0-232">Todos os utilizadores de Olá agora mostram Olá **resultados** lista.</span><span class="sxs-lookup"><span data-stu-id="41dc0-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="41dc0-233">Como adicionar mais dados, pode utilizar filtros toolimit os resultados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="41dc0-234">Por predefinição, o Explorador de dados utiliza `g.V()` tooretrieve todos os vértices num gráfico, mas podem alterar esse tooa diferentes [consulta gráfico](tutorial-query-graph.md), tais como `g.V().count()`, tooreturn uma contagem de todos os vértices Olá no gráfico de Olá no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="41dc0-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="41dc0-235">Agora, podemos ligar rakesh e ashley.</span><span class="sxs-lookup"><span data-stu-id="41dc0-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="41dc0-236">Certifique-se **ashley** no selecionado na Olá **resultados** lista, em seguida, clique no botão de edição Olá junto demasiado**destinos** no inferior direita.</span><span class="sxs-lookup"><span data-stu-id="41dc0-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="41dc0-237">Poderá ser necessário toowiden Olá de toosee a janela **propriedades** área.</span><span class="sxs-lookup"><span data-stu-id="41dc0-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Alterar o destino de Olá de um vértice num gráfico](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="41dc0-239">No Olá **destino** caixa tipo *rakesh*e em Olá **etiqueta Edge** caixa tipo *sabe*e, em seguida, clique em Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="41dc0-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Adicionar uma ligação entre ashley e rakesh no Data Explorer](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="41dc0-241">Agora selecionar **rakesh** da lista de resultados de Olá e ver se ashley e rakesh estão ligados.</span><span class="sxs-lookup"><span data-stu-id="41dc0-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Dois vértices ligados no Data Explorer](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="41dc0-243">Também pode utilizar os procedimentos de toocreate armazenado do Explorador de dados, UDFs e lógica de negócio do lado do servidor de tooperform de acionadores bem como o débito de escala.</span><span class="sxs-lookup"><span data-stu-id="41dc0-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="41dc0-244">Explorador de dados expõe todos os Olá incorporada programático acesso aos dados disponível no Olá APIs, mas fornece acesso fácil tooyour dados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41dc0-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="41dc0-245">Reveja os SLAs no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41dc0-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="41dc0-246">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="41dc0-246">Clean up resources</span></span>

<span data-ttu-id="41dc0-247">Se não toocontinue toouse esta aplicação, elimine todos os recursos criados por este guia de introdução no Olá portal do Azure com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="41dc0-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="41dc0-248">No menu da esquerda de Olá no Olá portal do Azure, clique em **grupos de recursos** e, em seguida, clique em nome de Olá do recurso de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="41dc0-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="41dc0-249">Na sua página de grupo de recursos, clique em **eliminar**, escreva o nome de Olá de Olá recursos toodelete na caixa de texto Olá e, em seguida, clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="41dc0-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41dc0-250">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="41dc0-250">Next steps</span></span>

<span data-ttu-id="41dc0-251">Este guia de introdução, aprendeu como criar um gráfico com o Explorador de dados de Olá toocreate uma conta de base de dados do Azure Cosmos e executar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="41dc0-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="41dc0-252">Agora, pode criar consultas mais complexas e implementar lógica poderosa para percorrer gráficos com Gremlin.</span><span class="sxs-lookup"><span data-stu-id="41dc0-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> <span data-ttu-id="41dc0-253">[Query using Gremlin](tutorial-query-graph.md) (Utilizar Gremlin para consultar)</span><span class="sxs-lookup"><span data-stu-id="41dc0-253">[Query using Gremlin](tutorial-query-graph.md)</span></span>

