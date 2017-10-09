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
# <a name="modeling-document-data-for-nosql-databases"></a>Modelação de dados de documento para bases de dados NoSQL
Enquanto sem esquema bases de dados, como a base de dados do Azure Cosmos facilitam super modelo dados tooembrace alterações tooyour ainda deve despesas em algumas tempo pensar sobre os dados. 

Como dados vai toobe armazenada? Como é os dados aplicação tooretrieve e consulta? É a sua aplicação heavy de leitura ou escrita pesada? 

Depois de ler este artigo, irá ser Olá tooanswer capaz de seguintes perguntas:

* Como necessário pensar sobre um documento numa base de dados de documento?
* O que é modelação de dados e por que motivo deve posso mais importantes para si? 
* Como é dados de modelação no documento da base de dados diferentes tooa base de dados relacional?
* Como posso express relações de dados numa base de dados não relacionais?
* Quando incorporar dados e quando associar toodata?

## <a name="embedding-data"></a>Ao incorporar dados
Quando inicia a modelação de dados num arquivo de documentos, tais como a base de dados do Azure Cosmos, tente tootreat as entidades como **documentos autónomo** representados no JSON.

Antes que explore demasiado muito além disso, informe-nos reponha alguns passos e ver como podemos poderá modelo algo na base de dados relacional, um assunto muitos dos EUA já estejam familiarizados com. Olá exemplo seguinte mostra como uma pessoa poderá ser armazenada na base de dados relacional. 

![Modelo de base de dados relacional](./media/documentdb-modeling-data/relational-data-model.png)

Ao trabalhar com bases de dados relacionais, iremos tiver sido taught para toonormalize anos, normalizar, normalizar.

Normalizing, normalmente, os dados envolve a uma entidade, tal como uma pessoa e danificando a para baixo no toodiscrete peças de dados. No exemplo de Olá acima, uma pessoa pode ter vários registos de detalhes de contacto, bem como vários registos de endereço. Ainda estamos aceda um passo adicional e dividir os detalhes de contacto extraindo mais comuns campos como um tipo. Mesmo para o endereço, cada registo aqui tem um tipo como *home page* ou *negócio* 

Olá, ao servir de no local quando normalizing dados é demasiado**evitar armazenar dados redundantes** em cada registo e, em vez disso, consulte toodata. Neste exemplo, tooread uma pessoa, com todos os respetivos detalhes de contacto e os endereços, terá de toouse associações tooeffectively agregar os dados em tempo de execução.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Atualizar uma única pessoa com os respetivos detalhes de contacto e endereços necessita de operações de escrita em várias tabelas individuais. 

Agora vamos tirar uma vista de olhos como podemos seria modelo Olá mesmo dados como uma entidade na base de dados de documento autónomo.

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

Utilizar a abordagem de Olá acima agora temos **denormalized** Olá registo pessoa onde iremos **incorporados** Olá todas as informações relacionadas com a pessoa toothis, como os respetivos detalhes de contacto e os endereços, tooa único Documento JSON.
Além disso, porque que não estão limitados tooa fixo esquema que temos aspetos de toodo de flexibilidade Olá como tendo os detalhes de contacto de diferentes formas completamente. 

Obter um registo de pessoa completa da base de dados de Olá está agora numa única operação em relação a uma única coleção e de um único documento de leitura. A atualização do registo de uma pessoa, com os respetivos detalhes de contacto e os endereços, também é uma operação de escrita única em relação a um único documento.

Por denormalizing dados, a aplicação poderá ter tooissue menos consultas e atualizações toocomplete operações comuns. 

### <a name="when-tooembed"></a>Quando tooembed
Em geral, utilize os dados incorporados modelos quando:

* Existem **contém** relações entre entidades.
* Existem **um-para-algumas** relações entre entidades.
* Não há dados incorporados que **alterações raramente**.
* É incorporado não aumentam dados **sem limite**.
* Não há dados incorporados, que é **integral** toodata num documento.

> [!NOTE]
> Normalmente desnormalizadas dados modelos fornecem melhor **ler** desempenho.
> 
> 

### <a name="when-not-tooembed"></a>Quando não tooembed
Enquanto Olá regra prática numa base de dados de documento é toodenormalize tudo e incorporar todos os dados tooa único documento, isto pode levar toosome situações que devem ser evitadas.

Colocar este fragmento JSON.

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

Isto pode dever uma entidade de post com comentários incorporados seria aspeto se podemos foram modelação um blogue típico ou CMS, sistema. Olá problema com este exemplo é essa Olá comentários matriz é **unbounded**, que significa que não há nenhum limite (prático) toohello diversas comentários pode ter qualquer post único. Isto irá tornar-se um problema como tamanho Olá documento Olá pode aumentar significativamente.

Como o tamanho de Olá de Olá documento crescimentos de dados de Olá Olá capacidade tootransmit durante a transmissão Olá, bem como a leitura e atualização documento de Olá, à escala, será afetado.

Neste caso, seria uma melhor tooconsider Olá, seguindo o modelo.

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

Este modelo tem Olá três mais recentes comentários incorporados no Olá próprio, o que é uma matriz com um limite fixo após esta hora. Olá outros comentários são agrupados numa toobatches de 100 comentários e armazenados nos documentos separados. o tamanho do lote de Olá Olá foi escolhido como 100 porque a nossa aplicação fictícia permite que Olá comentários do utilizador tooload 100 cada vez.  

Outro cenário onde incorporar dados não são uma boa ideia é quando Olá incorporado dados são utilizados frequentemente entre documentos e serão alterado frequentemente. 

Colocar este fragmento JSON.

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

Isto pode representar portefólio as cotações de uma pessoa. Escolhemos informações as cotações de Olá tooembed no documento de portefólio tooeach. Num ambiente onde dados relacionados mudam frequentemente, como um gráfico de cotações comerciais aplicação, ao incorporar dados que são alterados frequentemente vai toomean que lhe está constantemente a atualizar cada documento portefólio sempre que um gráfico de cotações é transacionado.

Gráfico de cotações *zaza* poderá ser transacionadas várias centenas de vezes numa única dia e milhares de utilizadores pode ter *zaza* no respetivo portefólio. Com um modelo de dados como Olá acima seria temos tooupdate muitos milhares de documentos portefólio demasiadas vezes todos os dias à esquerda tooa sistema que não escala muito bem. 

## <a id="Refer"></a>Dados de referência
Por isso, ao incorporar dados funciona bem para muitos casos, mas é claro que existem cenários quando denormalizing os dados fará com que problemas mais do que é importante. Por isso, o que podemos fazer agora? 

Bases de dados relacionais não são implementados apenas olá onde pode criar relações entre entidades. Numa base de dados de documento pode ter informações de um documento que, na verdade, está relacionada com toodata outros documentos. Agora, posso estou não advocating para um minuto, mesmo que iremos criar sistemas que seriam uma melhor se adequam tooa base de dados relacional do BD Azure Cosmos ou outra base de dados de documento, mas as relações simples podem ser utilizadas e podem ser bastante útil. 

No Olá JSON abaixo escolhemos de exemplo de Olá toouse de um portefólio as cotações de versões anteriores, mas desta vez, consulte toohello item as cotações no portefólio Olá em vez de incorporá-lo. Desta forma, quando o item as cotações Olá altera-se frequentemente ao longo Olá dia Olá apenas documento que necessita de toobe atualizado é o único documento as cotações de Olá. 

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


Uma abordagem de toothis downside imediata apesar está se a aplicação necessária tooshow informação sobre cada gráfico de cotações mantida quando se apresenta o portefólio de uma pessoa; Neste caso, terá de toomake vários viagens toohello da base de dados tooload Olá informações para cada documento as cotações. Aqui fizemos uma eficiência de Olá tooimprove decisão das operações de escrita, que ocorrem frequentemente ao longo do dia de Olá, mas por sua vez comprometida em Olá ler as operações poderão tem menor impacto no desempenho Olá deste sistema específico.

> [!NOTE]
> Modelos de dados de perdas **pode necessitar de ida e volta mais** toohello servidor.
> 
> 

### <a name="what-about-foreign-keys"></a>O que sobre chaves externas?
Porque não existe atualmente nenhum conceito de uma restrição, chave externa ou, caso contrário, quaisquer relações entre documentos que tenham documentos são eficazmente "ligações fracas" e não serão verificadas pela Olá própria base de dados. Se quiser tooensure Olá dados que faz referência um documento tooactually existe, terá então toodo esta na sua aplicação ou através da utilização de Olá de acionadores do lado do servidor ou procedimentos armazenados na base de dados do Azure Cosmos.

### <a name="when-tooreference"></a>Quando tooreference
Em geral, utilize dados normalizados modelos quando:

* Que representa **um-para-muitos** relações.
* Que representa **muitos-para-muitos** relações.
* Dados relacionados com **altera com frequência**.
* Pode ser referenciados dados **unbounded**.

> [!NOTE]
> Normalmente, normalizing fornece melhor **escrever** desempenho.
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Onde posso colocar relação Olá?
crescimento de Olá da relação de Olá irão ajudá-lo a determinar as referência do documento toostore Olá.

Se vamos ver Olá JSON abaixo modelos editores e books.

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

Se o número de Olá Books Olá por publicador é pequeno com o crescimento limitado, em seguida, o armazenamento de referência de livro Olá existente no documento de publicador Olá poderá ser útil. No entanto, se o número de Olá Books por publicador é unbounded, em seguida, este modelo de dados iria fazer toomutable, matrizes, como no documento de publicador de exemplo de Olá acima a crescer. 

Mudar coisas em torno de um bit seria estas coleções de grandes dimensões mutável evita de resultado de um modelo que representa ainda Olá mesmos dados, mas agora.

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

No Olá acima exemplo, vamos ignorou Olá coleção unbounded num documento do publicador Olá. Em vez disso, temos apenas um fabricante toohello referência em cada documento no livro.

### <a name="how-do-i-model-manymany-relationships"></a>Como posso modelar relações muitos:?
Na base de dados relacional *: muitos* relações são, muitas vezes, modeladas com tabelas de associação, que apenas associar registos da outras tabelas em conjunto. 

![Associar tabelas](./media/documentdb-modeling-data/join-table.png)

Poderá ser tempted tooreplicate Olá utilizando a mesma coisa documentos e produzir um modelo de dados que se pareça semelhante toohello seguinte.

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

Isto funciona. No entanto, carregamento ou um autor com os respetivos books ou carregar um livro com o respetivo autor sempre precisaria de, pelo menos, duas consultas adicionais na base de dados de Olá. Uma consulta toohello associar documento e, em seguida, outra consulta toofetch Olá real documento que está a ser associado. 

Se tudo está a fazer esta tabela de associação é gluing, em conjunto, dois tipos de dados, em seguida, por que motivo não removê-la completamente?
Considere Olá seguinte.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Agora, se posso tivesse um autor, sei imediatamente os livros que escrever e por outro lado se posso tinha um documento de livro carregado seria sei ids de Olá de Olá author(s). Isto poupa essa consulta intermediária relativamente à tabela de associação de Olá reduzir o número de hello do servidor de ida e volta a aplicação tem toomake. 

## <a id="WrapUp"></a>Modelos de dados de híbridos
Iremos agora de analisar incorporar (ou denormalizing) e dados de referência (ou normalizing), cada uma tem os respetivos upsides e cada uma tem os compromissos visto que tem. 

-Não sempre tiver toobe ou ou, não ser um pouco scared toomix coisas cópias de segurança. 

Com base nos padrões de utilização específicos e cargas de trabalho poderão existir casos onde a combinação de incorporado da aplicação e dados referenciada faz sentido e foi oportunidades potenciais toosimpler lógica da aplicação com o servidor menos arredondar viagens mantendo ainda um bom nível de desempenho .

Considere Olá seguinte JSON. 

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

Aqui iremos (sobretudo) tiver seguido modelo incorporado Olá, onde os dados de outras entidades estão incorporados no documento de nível superior de Olá, mas outros dados são referenciados. 

Se observar o documento de livro Olá, é possível ver alguns interessantes campos quando vamos ver matriz Olá autores. Não existe um *id* campo que é o campo de Olá utilizamos documento de autor de back-tooan toorefer, prática padrão num modelo normalizado, mas, em seguida, iremos também ter *nome* e *thumbnailUrl*. Iremos foi tiver apenas bloqueada com *id* e à esquerda Olá aplicação tooget qualquer informação adicional sobre este necessário do documento do respetivo autor Olá utilizando Olá "ligação", mas porque a nossa aplicação apresenta o nome do autor Olá e um imagem em miniatura com cada livro apresentado, pode guardar um servidor de toohello de ida e volta por livro numa lista, denormalizing **algumas** dados a partir do autor Olá.

Certifique-se, se alterar o nome do autor Olá ou pretendessem tooupdate os respetivos fotografia seria temos toogo uma atualização cada livro se alguma vez publicados, mas para a nossa aplicação, com base no pressuposto de Olá que autores não são alterados os respetivos nomes muito frequentemente, esta é uma estrutura aceitável decisão.  

Exemplo de Olá existem **previamente calculado agregados** valores toosave dispendiosa de processamento de uma operação de leitura. Exemplo de Olá, alguns dos dados de Olá incorporados Olá autor documento são os dados que são calculados em tempo de execução. Sempre que um novo livro for publicado, é criado um documento de livro **e** campo de countOfBooks Olá está a definir o valor de tooa calculado com base no número de Olá de documentos do livro que existem para um determinado autor. Esta otimização seria boa nos sistemas de muita leitura onde iremos suportar toodo computações no escritas na ordem toooptimize leituras.

Olá toohave capacidade é disponibilizado um modelo com campos calculados previamente porque a base de dados do Azure Cosmos suporta **transações de documentos múltiplos**. Vários arquivos de NoSQL não é possível fazer transações entre documentos e, por conseguinte, advocate decisões de conceção, como "sempre incorporar tudo" devido a limitação de toothis. Com o Azure Cosmos DB, pode utilizar acionadores do lado do servidor ou procedimentos armazenados que inserir books e atualizar os autores tudo dentro de uma transação ACID. Agora que não **ter** tooembed tudo no tooone documentar toobe basta certificar-se de que os dados permanecem consistentes.

## <a name="NextSteps"></a>Passos seguintes
takeaways maiores de Olá do artigo é toounderstand que dados de modelação num mundo sem esquema são tão importantes como alguma vez. 

Tal como não há nenhum toorepresent única forma de um conjunto de dados num ecrã, não há nenhum toomodel única forma os dados. Que precisa toounderstand a aplicação e a forma como irá produzir, consumir e processar dados Olá. Em seguida, aplicando algumas das Olá diretrizes aqui apresentadas, podem definir sobre como criar um modelo que satisfaz Olá necessidades imediata da sua aplicação. Quando as suas aplicações precisam toochange, pode tirar partido da flexibilidade de Olá de uma base de dados sem esquema tooembrace que alterar e evoluir facilmente o seu modelo de dados. 

toolearn mais informações sobre a BD do Cosmos do Azure, consulte o serviço de toohello [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) página. 

toounderstand como tooshard seus dados através de várias partições, consulte demasiado[criação de partições de dados na base de dados do Azure Cosmos](documentdb-partition-data.md). 
