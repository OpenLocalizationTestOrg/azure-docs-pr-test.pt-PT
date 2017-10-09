---
title: dados de documento aaaModeling para uma base de dados NoSQL | Microsoft Docs
description: "Saiba mais acerca da modelação de dados para bases de dados NoSQL"
keywords: "dados de modelação"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="6c518-104">Modelação de dados de documento para bases de dados NoSQL</span><span class="sxs-lookup"><span data-stu-id="6c518-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="6c518-105">Enquanto sem esquema bases de dados, como a base de dados do Azure Cosmos facilitam super modelo dados tooembrace alterações tooyour ainda deve despesas em algumas tempo pensar sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="6c518-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="6c518-106">Como dados vai toobe armazenada?</span><span class="sxs-lookup"><span data-stu-id="6c518-106">How is data going toobe stored?</span></span> <span data-ttu-id="6c518-107">Como é os dados aplicação tooretrieve e consulta?</span><span class="sxs-lookup"><span data-stu-id="6c518-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="6c518-108">É a sua aplicação heavy de leitura ou escrita pesada?</span><span class="sxs-lookup"><span data-stu-id="6c518-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="6c518-109">Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="6c518-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="6c518-110">Como necessário pensar sobre um documento numa base de dados de documento?</span><span class="sxs-lookup"><span data-stu-id="6c518-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="6c518-111">O que é modelação de dados e por que motivo deve posso mais importantes para si?</span><span class="sxs-lookup"><span data-stu-id="6c518-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="6c518-112">Como é dados de modelação no documento da base de dados diferentes tooa base de dados relacional?</span><span class="sxs-lookup"><span data-stu-id="6c518-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="6c518-113">Como posso express relações de dados numa base de dados não relacionais?</span><span class="sxs-lookup"><span data-stu-id="6c518-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="6c518-114">Quando incorporar dados e quando associar toodata?</span><span class="sxs-lookup"><span data-stu-id="6c518-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="6c518-115">Ao incorporar dados</span><span class="sxs-lookup"><span data-stu-id="6c518-115">Embedding data</span></span>
<span data-ttu-id="6c518-116">Quando inicia a modelação de dados num arquivo de documentos, tais como a base de dados do Azure Cosmos, tente tootreat as entidades como **documentos autónomo** representados no JSON.</span><span class="sxs-lookup"><span data-stu-id="6c518-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="6c518-117">Antes que explore demasiado muito além disso, informe-nos reponha alguns passos e ver como podemos poderá modelo algo na base de dados relacional, um assunto muitos dos EUA já estejam familiarizados com.</span><span class="sxs-lookup"><span data-stu-id="6c518-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="6c518-118">Olá exemplo seguinte mostra como uma pessoa poderá ser armazenada na base de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="6c518-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Modelo de base de dados relacional](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="6c518-120">Ao trabalhar com bases de dados relacionais, iremos tiver sido taught para toonormalize anos, normalizar, normalizar.</span><span class="sxs-lookup"><span data-stu-id="6c518-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="6c518-121">Normalizing, normalmente, os dados envolve a uma entidade, tal como uma pessoa e danificando a para baixo no toodiscrete peças de dados.</span><span class="sxs-lookup"><span data-stu-id="6c518-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="6c518-122">No exemplo de Olá acima, uma pessoa pode ter vários registos de detalhes de contacto, bem como vários registos de endereço.</span><span class="sxs-lookup"><span data-stu-id="6c518-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="6c518-123">Ainda estamos aceda um passo adicional e dividir os detalhes de contacto extraindo mais comuns campos como um tipo.</span><span class="sxs-lookup"><span data-stu-id="6c518-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="6c518-124">Mesmo para o endereço, cada registo aqui tem um tipo como *home page* ou *negócio*</span><span class="sxs-lookup"><span data-stu-id="6c518-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="6c518-125">Olá, ao servir de no local quando normalizing dados é demasiado**evitar armazenar dados redundantes** em cada registo e, em vez disso, consulte toodata.</span><span class="sxs-lookup"><span data-stu-id="6c518-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="6c518-126">Neste exemplo, tooread uma pessoa, com todos os respetivos detalhes de contacto e os endereços, terá de toouse associações tooeffectively agregar os dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6c518-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="6c518-127">Atualizar uma única pessoa com os respetivos detalhes de contacto e endereços necessita de operações de escrita em várias tabelas individuais.</span><span class="sxs-lookup"><span data-stu-id="6c518-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="6c518-128">Agora vamos tirar uma vista de olhos como podemos seria modelo Olá mesmo dados como uma entidade na base de dados de documento autónomo.</span><span class="sxs-lookup"><span data-stu-id="6c518-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="6c518-129">Utilizar a abordagem de Olá acima agora temos **denormalized** Olá registo pessoa onde iremos **incorporados** Olá todas as informações relacionadas com a pessoa toothis, como os respetivos detalhes de contacto e os endereços, tooa único Documento JSON.</span><span class="sxs-lookup"><span data-stu-id="6c518-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="6c518-130">Além disso, porque que não estão limitados tooa fixo esquema que temos aspetos de toodo de flexibilidade Olá como tendo os detalhes de contacto de diferentes formas completamente.</span><span class="sxs-lookup"><span data-stu-id="6c518-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="6c518-131">Obter um registo de pessoa completa da base de dados de Olá está agora numa única operação em relação a uma única coleção e de um único documento de leitura.</span><span class="sxs-lookup"><span data-stu-id="6c518-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="6c518-132">A atualização do registo de uma pessoa, com os respetivos detalhes de contacto e os endereços, também é uma operação de escrita única em relação a um único documento.</span><span class="sxs-lookup"><span data-stu-id="6c518-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="6c518-133">Por denormalizing dados, a aplicação poderá ter tooissue menos consultas e atualizações toocomplete operações comuns.</span><span class="sxs-lookup"><span data-stu-id="6c518-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="6c518-134">Quando tooembed</span><span class="sxs-lookup"><span data-stu-id="6c518-134">When tooembed</span></span>
<span data-ttu-id="6c518-135">Em geral, utilize os dados incorporados modelos quando:</span><span class="sxs-lookup"><span data-stu-id="6c518-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="6c518-136">Existem **contém** relações entre entidades.</span><span class="sxs-lookup"><span data-stu-id="6c518-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="6c518-137">Existem **um-para-algumas** relações entre entidades.</span><span class="sxs-lookup"><span data-stu-id="6c518-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="6c518-138">Não há dados incorporados que **alterações raramente**.</span><span class="sxs-lookup"><span data-stu-id="6c518-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="6c518-139">É incorporado não aumentam dados **sem limite**.</span><span class="sxs-lookup"><span data-stu-id="6c518-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="6c518-140">Não há dados incorporados, que é **integral** toodata num documento.</span><span class="sxs-lookup"><span data-stu-id="6c518-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="6c518-141">Normalmente desnormalizadas dados modelos fornecem melhor **ler** desempenho.</span><span class="sxs-lookup"><span data-stu-id="6c518-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="6c518-142">Quando não tooembed</span><span class="sxs-lookup"><span data-stu-id="6c518-142">When not tooembed</span></span>
<span data-ttu-id="6c518-143">Enquanto Olá regra prática numa base de dados de documento é toodenormalize tudo e incorporar todos os dados tooa único documento, isto pode levar toosome situações que devem ser evitadas.</span><span class="sxs-lookup"><span data-stu-id="6c518-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="6c518-144">Colocar este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="6c518-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="6c518-145">Isto pode dever uma entidade de post com comentários incorporados seria aspeto se podemos foram modelação um blogue típico ou CMS, sistema.</span><span class="sxs-lookup"><span data-stu-id="6c518-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="6c518-146">Olá problema com este exemplo é essa Olá comentários matriz é **unbounded**, que significa que não há nenhum limite (prático) toohello diversas comentários pode ter qualquer post único.</span><span class="sxs-lookup"><span data-stu-id="6c518-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="6c518-147">Isto irá tornar-se um problema como tamanho Olá documento Olá pode aumentar significativamente.</span><span class="sxs-lookup"><span data-stu-id="6c518-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="6c518-148">Como o tamanho de Olá de Olá documento crescimentos de dados de Olá Olá capacidade tootransmit durante a transmissão Olá, bem como a leitura e atualização documento de Olá, à escala, será afetado.</span><span class="sxs-lookup"><span data-stu-id="6c518-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="6c518-149">Neste caso, seria uma melhor tooconsider Olá, seguindo o modelo.</span><span class="sxs-lookup"><span data-stu-id="6c518-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="6c518-150">Este modelo tem Olá três mais recentes comentários incorporados no Olá próprio, o que é uma matriz com um limite fixo após esta hora.</span><span class="sxs-lookup"><span data-stu-id="6c518-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="6c518-151">Olá outros comentários são agrupados numa toobatches de 100 comentários e armazenados nos documentos separados.</span><span class="sxs-lookup"><span data-stu-id="6c518-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="6c518-152">o tamanho do lote de Olá Olá foi escolhido como 100 porque a nossa aplicação fictícia permite que Olá comentários do utilizador tooload 100 cada vez.</span><span class="sxs-lookup"><span data-stu-id="6c518-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="6c518-153">Outro cenário onde incorporar dados não são uma boa ideia é quando Olá incorporado dados são utilizados frequentemente entre documentos e serão alterado frequentemente.</span><span class="sxs-lookup"><span data-stu-id="6c518-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="6c518-154">Colocar este fragmento JSON.</span><span class="sxs-lookup"><span data-stu-id="6c518-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="6c518-155">Isto pode representar portefólio as cotações de uma pessoa.</span><span class="sxs-lookup"><span data-stu-id="6c518-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="6c518-156">Escolhemos informações as cotações de Olá tooembed no documento de portefólio tooeach.</span><span class="sxs-lookup"><span data-stu-id="6c518-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="6c518-157">Num ambiente onde dados relacionados mudam frequentemente, como um gráfico de cotações comerciais aplicação, ao incorporar dados que são alterados frequentemente vai toomean que lhe está constantemente a atualizar cada documento portefólio sempre que um gráfico de cotações é transacionado.</span><span class="sxs-lookup"><span data-stu-id="6c518-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="6c518-158">Gráfico de cotações *zaza* poderá ser transacionadas várias centenas de vezes numa única dia e milhares de utilizadores pode ter *zaza* no respetivo portefólio.</span><span class="sxs-lookup"><span data-stu-id="6c518-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="6c518-159">Com um modelo de dados como Olá acima seria temos tooupdate muitos milhares de documentos portefólio demasiadas vezes todos os dias à esquerda tooa sistema que não escala muito bem.</span><span class="sxs-lookup"><span data-stu-id="6c518-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="6c518-160"><a id="Refer"></a>Dados de referência</span><span class="sxs-lookup"><span data-stu-id="6c518-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="6c518-161">Por isso, ao incorporar dados funciona bem para muitos casos, mas é claro que existem cenários quando denormalizing os dados fará com que problemas mais do que é importante.</span><span class="sxs-lookup"><span data-stu-id="6c518-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="6c518-162">Por isso, o que podemos fazer agora?</span><span class="sxs-lookup"><span data-stu-id="6c518-162">So what do we do now?</span></span> 

<span data-ttu-id="6c518-163">Bases de dados relacionais não são implementados apenas olá onde pode criar relações entre entidades.</span><span class="sxs-lookup"><span data-stu-id="6c518-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="6c518-164">Numa base de dados de documento pode ter informações de um documento que, na verdade, está relacionada com toodata outros documentos.</span><span class="sxs-lookup"><span data-stu-id="6c518-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="6c518-165">Agora, posso estou não advocating para um minuto, mesmo que iremos criar sistemas que seriam uma melhor se adequam tooa base de dados relacional do BD Azure Cosmos ou outra base de dados de documento, mas as relações simples podem ser utilizadas e podem ser bastante útil.</span><span class="sxs-lookup"><span data-stu-id="6c518-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="6c518-166">No Olá JSON abaixo escolhemos de exemplo de Olá toouse de um portefólio as cotações de versões anteriores, mas desta vez, consulte toohello item as cotações no portefólio Olá em vez de incorporá-lo.</span><span class="sxs-lookup"><span data-stu-id="6c518-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="6c518-167">Desta forma, quando o item as cotações Olá altera-se frequentemente ao longo Olá dia Olá apenas documento que necessita de toobe atualizado é o único documento as cotações de Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="6c518-168">Uma abordagem de toothis downside imediata apesar está se a aplicação necessária tooshow informação sobre cada gráfico de cotações mantida quando se apresenta o portefólio de uma pessoa; Neste caso, terá de toomake vários viagens toohello da base de dados tooload Olá informações para cada documento as cotações.</span><span class="sxs-lookup"><span data-stu-id="6c518-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="6c518-169">Aqui fizemos uma eficiência de Olá tooimprove decisão das operações de escrita, que ocorrem frequentemente ao longo do dia de Olá, mas por sua vez comprometida em Olá ler as operações poderão tem menor impacto no desempenho Olá deste sistema específico.</span><span class="sxs-lookup"><span data-stu-id="6c518-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="6c518-170">Modelos de dados de perdas **pode necessitar de ida e volta mais** toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="6c518-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="6c518-171">O que sobre chaves externas?</span><span class="sxs-lookup"><span data-stu-id="6c518-171">What about foreign keys?</span></span>
<span data-ttu-id="6c518-172">Porque não existe atualmente nenhum conceito de uma restrição, chave externa ou, caso contrário, quaisquer relações entre documentos que tenham documentos são eficazmente "ligações fracas" e não serão verificadas pela Olá própria base de dados.</span><span class="sxs-lookup"><span data-stu-id="6c518-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="6c518-173">Se quiser tooensure Olá dados que faz referência um documento tooactually existe, terá então toodo esta na sua aplicação ou através da utilização de Olá de acionadores do lado do servidor ou procedimentos armazenados na base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6c518-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="6c518-174">Quando tooreference</span><span class="sxs-lookup"><span data-stu-id="6c518-174">When tooreference</span></span>
<span data-ttu-id="6c518-175">Em geral, utilize dados normalizados modelos quando:</span><span class="sxs-lookup"><span data-stu-id="6c518-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="6c518-176">Que representa **um-para-muitos** relações.</span><span class="sxs-lookup"><span data-stu-id="6c518-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="6c518-177">Que representa **muitos-para-muitos** relações.</span><span class="sxs-lookup"><span data-stu-id="6c518-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="6c518-178">Dados relacionados com **altera com frequência**.</span><span class="sxs-lookup"><span data-stu-id="6c518-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="6c518-179">Pode ser referenciados dados **unbounded**.</span><span class="sxs-lookup"><span data-stu-id="6c518-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c518-180">Normalmente, normalizing fornece melhor **escrever** desempenho.</span><span class="sxs-lookup"><span data-stu-id="6c518-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="6c518-181">Onde posso colocar relação Olá?</span><span class="sxs-lookup"><span data-stu-id="6c518-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="6c518-182">crescimento de Olá da relação de Olá irão ajudá-lo a determinar as referência do documento toostore Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="6c518-183">Se vamos ver Olá JSON abaixo modelos editores e books.</span><span class="sxs-lookup"><span data-stu-id="6c518-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="6c518-184">Se o número de Olá Books Olá por publicador é pequeno com o crescimento limitado, em seguida, o armazenamento de referência de livro Olá existente no documento de publicador Olá poderá ser útil.</span><span class="sxs-lookup"><span data-stu-id="6c518-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="6c518-185">No entanto, se o número de Olá Books por publicador é unbounded, em seguida, este modelo de dados iria fazer toomutable, matrizes, como no documento de publicador de exemplo de Olá acima a crescer.</span><span class="sxs-lookup"><span data-stu-id="6c518-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="6c518-186">Mudar coisas em torno de um bit seria estas coleções de grandes dimensões mutável evita de resultado de um modelo que representa ainda Olá mesmos dados, mas agora.</span><span class="sxs-lookup"><span data-stu-id="6c518-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="6c518-187">No Olá acima exemplo, vamos ignorou Olá coleção unbounded num documento do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="6c518-188">Em vez disso, temos apenas um fabricante toohello referência em cada documento no livro.</span><span class="sxs-lookup"><span data-stu-id="6c518-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="6c518-189">Como posso modelar relações muitos:?</span><span class="sxs-lookup"><span data-stu-id="6c518-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="6c518-190">Na base de dados relacional *: muitos* relações são, muitas vezes, modeladas com tabelas de associação, que apenas associar registos da outras tabelas em conjunto.</span><span class="sxs-lookup"><span data-stu-id="6c518-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Associar tabelas](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="6c518-192">Poderá ser tempted tooreplicate Olá utilizando a mesma coisa documentos e produzir um modelo de dados que se pareça semelhante toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="6c518-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="6c518-193">Isto funciona.</span><span class="sxs-lookup"><span data-stu-id="6c518-193">This would work.</span></span> <span data-ttu-id="6c518-194">No entanto, carregamento ou um autor com os respetivos books ou carregar um livro com o respetivo autor sempre precisaria de, pelo menos, duas consultas adicionais na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="6c518-195">Uma consulta toohello associar documento e, em seguida, outra consulta toofetch Olá real documento que está a ser associado.</span><span class="sxs-lookup"><span data-stu-id="6c518-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="6c518-196">Se tudo está a fazer esta tabela de associação é gluing, em conjunto, dois tipos de dados, em seguida, por que motivo não removê-la completamente?</span><span class="sxs-lookup"><span data-stu-id="6c518-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="6c518-197">Considere Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="6c518-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="6c518-198">Agora, se posso tivesse um autor, sei imediatamente os livros que escrever e por outro lado se posso tinha um documento de livro carregado seria sei ids de Olá de Olá author(s).</span><span class="sxs-lookup"><span data-stu-id="6c518-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="6c518-199">Isto poupa essa consulta intermediária relativamente à tabela de associação de Olá reduzir o número de hello do servidor de ida e volta a aplicação tem toomake.</span><span class="sxs-lookup"><span data-stu-id="6c518-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="6c518-200"><a id="WrapUp"></a>Modelos de dados de híbridos</span><span class="sxs-lookup"><span data-stu-id="6c518-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="6c518-201">Iremos agora de analisar incorporar (ou denormalizing) e dados de referência (ou normalizing), cada uma tem os respetivos upsides e cada uma tem os compromissos visto que tem.</span><span class="sxs-lookup"><span data-stu-id="6c518-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="6c518-202">-Não sempre tiver toobe ou ou, não ser um pouco scared toomix coisas cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="6c518-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="6c518-203">Com base nos padrões de utilização específicos e cargas de trabalho poderão existir casos onde a combinação de incorporado da aplicação e dados referenciada faz sentido e foi oportunidades potenciais toosimpler lógica da aplicação com o servidor menos arredondar viagens mantendo ainda um bom nível de desempenho .</span><span class="sxs-lookup"><span data-stu-id="6c518-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="6c518-204">Considere Olá seguinte JSON.</span><span class="sxs-lookup"><span data-stu-id="6c518-204">Consider hello following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="6c518-205">Aqui iremos (sobretudo) tiver seguido modelo incorporado Olá, onde os dados de outras entidades estão incorporados no documento de nível superior de Olá, mas outros dados são referenciados.</span><span class="sxs-lookup"><span data-stu-id="6c518-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="6c518-206">Se observar o documento de livro Olá, é possível ver alguns interessantes campos quando vamos ver matriz Olá autores.</span><span class="sxs-lookup"><span data-stu-id="6c518-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="6c518-207">Não existe um *id* campo que é o campo de Olá utilizamos documento de autor de back-tooan toorefer, prática padrão num modelo normalizado, mas, em seguida, iremos também ter *nome* e *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="6c518-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="6c518-208">Iremos foi tiver apenas bloqueada com *id* e à esquerda Olá aplicação tooget qualquer informação adicional sobre este necessário do documento do respetivo autor Olá utilizando Olá "ligação", mas porque a nossa aplicação apresenta o nome do autor Olá e um imagem em miniatura com cada livro apresentado, pode guardar um servidor de toohello de ida e volta por livro numa lista, denormalizing **algumas** dados a partir do autor Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="6c518-209">Certifique-se, se alterar o nome do autor Olá ou pretendessem tooupdate os respetivos fotografia seria temos toogo uma atualização cada livro se alguma vez publicados, mas para a nossa aplicação, com base no pressuposto de Olá que autores não são alterados os respetivos nomes muito frequentemente, esta é uma estrutura aceitável decisão.</span><span class="sxs-lookup"><span data-stu-id="6c518-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="6c518-210">Exemplo de Olá existem **previamente calculado agregados** valores toosave dispendiosa de processamento de uma operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="6c518-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="6c518-211">Exemplo de Olá, alguns dos dados de Olá incorporados Olá autor documento são os dados que são calculados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6c518-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="6c518-212">Sempre que um novo livro for publicado, é criado um documento de livro **e** campo de countOfBooks Olá está a definir o valor de tooa calculado com base no número de Olá de documentos do livro que existem para um determinado autor.</span><span class="sxs-lookup"><span data-stu-id="6c518-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="6c518-213">Esta otimização seria boa nos sistemas de muita leitura onde iremos suportar toodo computações no escritas na ordem toooptimize leituras.</span><span class="sxs-lookup"><span data-stu-id="6c518-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="6c518-214">Olá toohave capacidade é disponibilizado um modelo com campos calculados previamente porque a base de dados do Azure Cosmos suporta **transações de documentos múltiplos**.</span><span class="sxs-lookup"><span data-stu-id="6c518-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="6c518-215">Vários arquivos de NoSQL não é possível fazer transações entre documentos e, por conseguinte, advocate decisões de conceção, como "sempre incorporar tudo" devido a limitação de toothis.</span><span class="sxs-lookup"><span data-stu-id="6c518-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="6c518-216">Com o Azure Cosmos DB, pode utilizar acionadores do lado do servidor ou procedimentos armazenados que inserir books e atualizar os autores tudo dentro de uma transação ACID.</span><span class="sxs-lookup"><span data-stu-id="6c518-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="6c518-217">Agora que não **ter** tooembed tudo no tooone documentar toobe basta certificar-se de que os dados permanecem consistentes.</span><span class="sxs-lookup"><span data-stu-id="6c518-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="6c518-218"><a name="NextSteps"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6c518-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="6c518-219">takeaways maiores de Olá do artigo é toounderstand que dados de modelação num mundo sem esquema são tão importantes como alguma vez.</span><span class="sxs-lookup"><span data-stu-id="6c518-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="6c518-220">Tal como não há nenhum toorepresent única forma de um conjunto de dados num ecrã, não há nenhum toomodel única forma os dados.</span><span class="sxs-lookup"><span data-stu-id="6c518-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="6c518-221">Que precisa toounderstand a aplicação e a forma como irá produzir, consumir e processar dados Olá.</span><span class="sxs-lookup"><span data-stu-id="6c518-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="6c518-222">Em seguida, aplicando algumas das Olá diretrizes aqui apresentadas, podem definir sobre como criar um modelo que satisfaz Olá necessidades imediata da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="6c518-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="6c518-223">Quando as suas aplicações precisam toochange, pode tirar partido da flexibilidade de Olá de uma base de dados sem esquema tooembrace que alterar e evoluir facilmente o seu modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="6c518-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="6c518-224">toolearn mais informações sobre a BD do Cosmos do Azure, consulte o serviço de toohello [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="6c518-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="6c518-225">toounderstand como tooshard seus dados através de várias partições, consulte demasiado[criação de partições de dados na base de dados do Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6c518-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
