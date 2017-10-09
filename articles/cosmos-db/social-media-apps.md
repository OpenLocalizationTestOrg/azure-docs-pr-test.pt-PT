---
title: "Padrão de conceção do Cosmos BD do Azure: aplicações de redes sociais | Microsoft Docs"
description: "Saiba mais sobre um padrão de conceção para as redes sociais, tirando partido flexibilidade de armazenamento de Olá de base de dados do Azure Cosmos e outros serviços do Azure."
keywords: "Aplicações de redes sociais"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Vai sociais com base de dados do Azure Cosmos
Living num society em massa interligadas significa que, num ponto da vida, passam a fazer parte de um **rede social**. Podemos utilizar redes sociais tookeep entre em contacto com amigos, colegas, família ou, por vezes, tooshare nosso passion com pessoas com interesses comuns.

Como engenheiros ou os programadores, iremos poderá wondered como estas redes armazenar e interligar-se nossos dados, ou poderá ter mesmo foi toocreate a tarefa ou arquiteto de sistemas uma nova rede social para um niche específico market yourselves. Que é quando for pergunta grande Olá: como a todos os dados são armazenados?

Vamos imaginar que estamos a criar uma novo e shiny rede social, onde os nossos utilizadores podem publicar artigos com suporte de dados relacionados, como, fotografias, vídeos ou até mesmo música. Os utilizadores podem comentar publicações e forneça pontos para as classificações. Existirá um feed de mensagens que os utilizadores irão ver e ser capaz de toointeract na página de destino principal Web site Olá. Isto não som realmente complexo (inicialmente), mas para sake Olá de simplicidade, vamos parar existe (Iremos foi delve para feeds personalizadas do utilizador afetados por relações, mas excede objetivo Olá deste artigo).

Por isso, como podemos armazenar esta e onde?

Muitos dos poderão ter experiência em bases de dados do SQL Server ou ter, pelo menos, a noção de [modelação de dados relacional](https://en.wikipedia.org/wiki/Relational_model) e poderá ser toostart tempted desenho algo semelhante ao seguinte:

![Diagrama que ilustra um modelo de relacional relativo](./media/social-media-apps/social-media-apps-sql.png) 

Uma estrutura de dados perfeitamente normalizado e pretty... que não a escala. 

Não obter-me o problema, posso já trabalhou com bases de dados SQL, de todos os meus vida, são excelente, mas como cada plataforma padrão, prática e software, não é perfeita para cada cenário.

Por que motivo não é melhor opção da SQL Olá neste cenário? Vamos observar a estrutura de Olá de um pedido de post único, se pretendesse posso tooshow publicar num Web site ou aplicação, seria necessário toodo uma consulta com... tabela 8 associações (!) tooshow apenas um único post, agora, imagem de um fluxo de mensagens que dinamicamente carregar e são apresentados num ecrã Olá e poderá ver onde vou.

Foi, obviamente, utilizamos uma instância do SQL humongous com suficiente toosolve de energia milhares de consultas com estes tooserve associações muitos nosso conteúdo, mas verdadeiramente, motivo pelo qual seria é quando uma solução mais simples existe?

## <a name="hello-nosql-road"></a>viagem de NoSQL Olá
Este artigo irá guiá-lo para a modelação de dados da sua plataforma de redes sociais com base de dados do Azure NoSQL [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) de forma económica, tirando partido de outras funcionalidades de base de dados do Azure Cosmos como Olá [Gremlin Graph API ](../cosmos-db/graph-introduction.md). Utilizar um [NoSQL](https://en.wikipedia.org/wiki/NoSQL) abordagem, armazenamento de dados no formato JSON e aplicar [denormalization](https://en.wikipedia.org/wiki/Denormalization), nosso post complicada anteriormente pode ser transformado numa única [documento](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

E pode ser obtido com uma única consulta e com nenhuma associações. Isto é muito mais simples e fácil e budget-wise, requer menos recursos tooachieve um resultado melhor.

BD do Azure do Cosmos certifica-se de que todas as propriedades de Olá são indexadas com o respetivo indexação automática, que pode ser mesmo [personalizado](indexing-policies.md). Olá sem esquema abordagem permite-na armazenar documentos com diferentes e dinâmicas estruturas, talvez amanhã que queremos toohave cronologia processará uma lista de categorias nem hashtags associados aos mesmos, Cosmos DB Olá novos documentos com Olá adicionar atributos com nenhuma adicionais trabalho necessário por-nos.

Comentários sobre um pedido post podem ser tratados como apenas outras mensagens com uma propriedade principal (Isto simplifica o nosso mapeamento de objeto). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

E todas as interações de redes sociais podem ser armazenadas num objeto separado como contadores:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

A criação de feeds é apenas um fim de criação de documentos que podem conter uma lista de ids de post com uma ordem de relevância especificado:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Foi temos uma transmissão em fluxo "mais recente" com mensagens ordenadas por data de criação, uma sequência "hottest" com as mensagens com mais likes no Olá últimas 24 horas, temos mesmo foi possível implementar uma sequência personalizada para cada utilizador com base na lógica como followers e interesses e ainda seria uma lista de  publicações. É um independentemente de como toobuild estas listas, mas o desempenho de leitura de Olá permanece unhindered. Assim que iremos adquirir uma destas listas, iremos emitir tooCosmos uma única consulta DB utilizando Olá [no operador](documentdb-sql-query.md#WhereClause) tooobtain páginas de mensagens de cada vez.

Olá feed fluxos pode ser criada utilizando [dos serviços de aplicações do Azure](https://azure.microsoft.com/services/app-service/) em segundo plano processos: [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Quando um pedido post for criado, o processamento em segundo plano pode ser acionado utilizando [Storage do Azure](https://azure.microsoft.com/services/storage/) [filas](../storage/queues/storage-dotnet-how-to-use-queues.md) e Webjobs acionadas utilizando Olá [SDK de Webjobs do Azure](../app-service-web/websites-dotnet-webjobs-sdk.md), implementar Olá após a propagação dentro de fluxos com base na nossa própria lógica personalizada. 

Pontos e likes através de um pedido post podem ser processados de forma diferida utilizando este toocreate técnica mesmo ambiente eventualmente consistente.

Followers são trickier. Cosmos DB tem um limite de tamanho máximo do documento e leitura/escrita documentos grandes podem afetar a escalabilidade de Olá da sua aplicação. Por isso, pode pensar sobre o armazenamento followers como um documento com esta estrutura:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Isto poderá funcionar para um utilizador com milhares de alguns followers, mas se alguns celebrity associa nosso ranks, esta abordagem direciona o tamanho do documento grande tooa e poderá tamanho do documento Olá eventualmente acessos cap.

toosolve, podemos utilizar uma abordagem mista. Como parte do documento de estatísticas de utilizadores Olá armazenamos número de Olá de followers:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

E gráfico de real Olá do followers pode ser armazenado utilizando a base de dados do Azure Cosmos [Gremlin Graph API](../cosmos-db/graph-introduction.md), toocreate [vertexes](http://mathworld.wolfram.com/GraphVertex.html) para cada utilizador e [contornos](http://mathworld.wolfram.com/GraphEdge.html) que manter Olá " Relações de forma-A-B". Olá Graph API permite-lhe não só obter followers Olá de um determinado utilizador como criar consultas mais complexas tooeven sugerir pessoas em comum. Se adicionamos Olá de gráfico toohello categorias de conteúdo que as pessoas gosta ou desfrutar, podemos começar weaving experiências que incluem a deteção de conteúdos inteligente, sugerindo conteúdo que aqueles que siga como ou localizar pessoas com quem pode temos muito em comum.

documento de estatísticas de utilizadores Olá pode ainda ser cartões toocreate utilizados no Olá IU ou pré-visualizações de perfil rápida.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Olá duplicação de dados e padrão "Ladder"
Como poderá ter reparado no documento JSON Olá que faça referência a um pedido post, existem várias ocorrências de um utilizador. E seria ter adivinhado direita, que isto significa que as informações de Olá que representa fornecido por este denormalization, um utilizador poderão estar presentes em mais do que um local.

Na ordem tooallow para consultas mais rápidas, iremos implicar duplicação de dados. problema de Olá com este efeito é que, se por alguma ação, alterações de dados de um utilizador, precisamos toofind todas as atividades de Olá ele nunca foi e atualizá-las todas as. Não som muito prática, direita?

Estamos toosolve contínuo Olá-lo por identificar os atributos de chave de um utilizador que iremos mostrar na nossa aplicação para cada atividade. Se visualmente vamos mostrar um pedido post na nossa aplicação e mostrar apenas do criador de Olá nome e a imagem, motivo pelo qual armazenar todos os dados do utilizador Olá no atributo de revisão criada Olá "por"? Se para cada comentário mostramos apenas imagem do utilizador Olá, realmente já não precisamos restante Olá as informações. É onde algo que posso chamar Olá "Ladder padrão de" entra em play.

Vamos informações de utilizador como um exemplo:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Ao observar estas informações, pode rapidamente detectarmos que é informações importantes e que, por conseguinte, não se encontra, criar um "Ladder":

![Diagrama de um padrão de ladder](./media/social-media-apps/social-media-apps-ladder.png)

passo menor Olá é chamado um UserChunk, o elemento de mínima Olá de informação que identifica um utilizador e é utilizada para dados duplicados. Ao reduzir o tamanho de Olá duplicado dados tooonly Olá informações vamos "Mostrar" Olá, estamos a reduzir a possibilidade de Olá de atualizações em grande escala.

passo média Olá é designado por utilizador Olá, é dados completa Olá que vão ser utilizados na maior parte das consultas dependentes de desempenho na base de dados do Cosmos, hello mais acedidos e crítico. Inclui informações de Olá representadas por um UserChunk.

Olá, maior é Olá utilizador expandida. Inclui todas as informações de utilizador críticos Olá e outros dados que realmente não requerem rapidamente toobe leitura ou de utilização é eventual (por exemplo, o processo de início de sessão de Olá). Estes dados podem ser armazenados fora do Cosmos DB, na SQL Database do Azure ou tabelas de armazenamento do Azure.

Por que motivo seria iremos dividir utilizador Olá e até mesmo armazenar estas informações em locais diferentes? Porque um desempenho ponto de vista de Olá maiores documentos de Olá, Olá costlier consultas de Olá. Manter documentos slim, com Olá direita informações toodo todos os seus desempenho dependentes da consulta para a sua rede social e arquivo Olá outras informações adicionais para o eventual cenários, como, as edições do perfil completo, inícios de sessão, mesmo a extração de dados para análise de utilização e Big Iniciativas de dados. Iremos realmente não mais importantes para si se for mais lentos Olá recolha de dados de extração de dados porque está em execução na base de dados do Azure SQL, podemos ter concern apesar que os nossos utilizadores tenham uma experiência de slim e rápida. Um utilizador, armazenado na base de dados do Cosmos, deverá ter o seguinte aspeto:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

E um pedido Post deverá ter o seguinte aspeto:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

E quando uma edição acontecer onde um dos atributos de Olá de segmento de Olá foi afetado, é fácil toofind documentos de Olá afetado utilizando consultas que apontam toohello indexada atributos (SELECIONAR * FROM mensagens p onde p.createdBy.id = = "edited_user_id") e, em seguida, atualizar segmentos Olá.

## <a name="hello-search-box"></a>caixa de pesquisa de Olá
Os utilizadores irão gerar, luckily, muito do conteúdo. E deve ser capaz de tooprovide Olá capacidade toosearch e localizar conteúdo que poderá não ser diretamente no respetivos conteúdos fluxos, talvez porque foi não segue criadores de Olá ou talvez iremos estiver apenas a tentar toofind esse post antigo que fizemos há de 6 meses.

Thankfully, e porque está a utilizar BD do Cosmos do Azure, pode facilmente implementar um motor de pesquisa utilizando [da Azure Search](https://azure.microsoft.com/services/search/) em alguns minutos e sem escrever uma única linha de código (exceto Olá obviamente, pesquise processo e IU).

Por que motivo é por isso, fácil?

A Azure Search implementa que chamarem [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx), em segundo plano processa esse hook nos seus repositórios de dados e automagically adicionar, atualizar ou remover os objetos em índices Olá. Suportam um [indexadores de base de dados do Azure SQL](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [indexadores de Blobs do Azure](../search/search-howto-indexing-azure-blob-storage.md) e thankfully, [indexadores de base de dados do Azure Cosmos](../search/search-howto-index-documentdb.md). Olá transição das informações da base de dados do Cosmos tooAzure pesquisa é simples, como as informações de arquivo no formato JSON, precisamos apenas de demasiado[criar nosso índice](../search/search-create-index-portal.md) e mapear os atributos a partir dos nossos documentos queremos indexadas e que é num fim de minutos (depende do tamanho Olá dos nossos dados,) todo o nosso conteúdo estará disponível toobe pesquisado após, por Olá melhor pesquisa-como-um-serviço solução na infraestrutura de nuvem. 

Para obter mais informações sobre a Azure Search, pode visitar Olá [tooSearch de guia do Hitchhiker](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>dados de conhecimento subjacente Olá
Depois de armazenar este conteúdo que aumenta e o crescimentos de todos os dias, poderá encontrámos ourselves pensar: o que posso fazer com todos os este fluxo de informações dos meus utilizadores?

resposta de Olá é simples: colocá-la toowork e obter informações a partir do mesmo.

No entanto, o que podemos saber? Alguns exemplos de fácil incluem [análise de dados de sentimento](https://en.wikipedia.org/wiki/Sentiment_analysis), conteúdo recomendações com base nas preferências de um utilizador ou mesmo uma automatizada conteúdo moderator que garante que todos os conteúdos publicados pelo nossa rede social de Olá é seguro para Olá família.

Agora que tem posso que estabelecer ligação com ele, provavelmente irá considerar terá algumas PhD em bibliotecas ciência tooextract estes padrões e as informações fora de bases de dados simples e ficheiros, mas seria errado.

[O Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), que fazem parte da Olá [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), é Olá um serviço em nuvem completamente gerido que lhe permite criar fluxos de trabalho utilizando algoritmos numa interface de arrastar e largar simples, os suas próprias algoritmos de código no [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) ou utilizar algumas das Olá já criadas e pronto toouse APIs, tais como: [análise de texto](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [Moderator conteúdo](https://www.microsoft.com/moderator) ou [recomendações](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve qualquer um destes cenários de Machine Learning, podemos utilizar [do Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest Olá informações a partir de diferentes origens e utilizar [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess Olá informações e gerar uma saída que podem ser processados pelo Azure Machine Learning.

Outra opção disponível é toouse [serviços cognitivos Microsoft](https://www.microsoft.com/cognitive-services) tooanalyze nossos utilizadores conteúdos; não apenas os que compreender melhor (através da análise escrever com [API de análise de texto](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), mas Iremos também foi detete conteúdo madura ou indesejável e agir em conformidade com [computador visão API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Serviços cognitivos incluem muitas das soluções de out of box, que não necessitam de qualquer tipo de toouse de dados de conhecimento do Machine Learning.

## <a name="a-planet-scale-social-experience"></a>Uma experiência de redes sociais planet escala
Existe um último, mas não pelo menos, tópico importante posso devem ser abordadas: **escalabilidade**. Ao conceber uma arquitetura é fundamental que cada componente pode dimensionar no seu próprio, ou porque precisamos tooprocess mais dados ou uma vez que queremos toohave uma maior cobertura geográfica (ou ambos!). Thankfully, alcançar uma tarefa complexa é um **experiência chave na mão** com base de dados do Cosmos.

Suporte cosmos DB [criação dinâmica de partições](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-a-box criando automaticamente partições com base num determinado **chave de partição** (definido como um dos atributos de Olá no seus documentos). Definir Olá correto de chave de partição tem de ser efetuada no momento da conceção e mantém no Olá atenção [melhores práticas](../cosmos-db/partition-data.md#designing-for-partitioning) disponíveis; no caso de Olá de uma experiência de redes social, a estratégia de criação de partições têm de estar alinhada com a forma de Olá consultar (leituras dentro do Olá a mesma partição são desejável) e de escrita (evitar "frequente oportunidades" pelo escritas em várias partições). Algumas opções são: partições com base numa chave temporal (dia/mês/semana), por categoria de conteúdo, por região geográfica, por utilizador; todas as realmente depende de como irá consultar dados Olá e mostrá-lo na sua experiência de redes social. 

Um ponto interessante mencionar é que a BD do Cosmos irá executar as suas consultas (incluindo [agregados](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) em todas as partições de forma transparente, não precisa de tooadd qualquer lógica à medida que aumenta os dados.

Com a hora, eventualmente irá aumentar no tráfego e o consumo de recursos (medido em [RUs](request-units.md), ou unidades de pedido) irá aumentar. Será de leitura e escrita mais frequentemente como seu userbase cresce e começará a criar e ler mais conteúdos; Olá, capacidade de **aumentar o débito** é vital. Aumentar o nosso RUs é muito fácil, podemos fazer com alguns cliques no Portal do Azure de Olá ou por [emitir comandos através da API de Olá](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Como aumentar verticalmente e definir uma chave de partição](./media/social-media-apps/social-media-apps-scaling.png)

O que acontece se coisas mantém a melhorar e os utilizadores de outra região, país ou continente, tenha em atenção a plataforma e comece a utilizá-la, que um excelente surprise!

Mas, aguarde..., logo que tenha em consideração as suas experiências com a plataforma não é o ideal; são até ao momento na direção oposta ao sua região operacional que a latência de Olá terríveis e que obviamente não quer que eles tooquit. Se apenas Ocorreu uma forma fácil de **expandir o alcance global**... mas não existe!

Cosmos DB permite-lhe [replicar os dados globalmente](../cosmos-db/tutorial-global-distribution-documentdb.md) e transparente com alguns cliques e automaticamente, selecione entre regiões Olá da sua [código de cliente](../cosmos-db/tutorial-global-distribution-documentdb.md). Isto também significa que pode fazer com que [várias regiões de ativação pós-falha](regional-failover.md). 

Quando se replica os dados globalmente, terá de toomake certificar-se de que os clientes podem tirar partido dos mesmos. Se estiver a utilizar um front-end de web ou accesing APIs a partir de clientes móveis, pode implementar [Traffic Manager do Azure](https://azure.microsoft.com/services/traffic-manager/) e clonar o App Service do Azure em todas as regiões de Olá assim o desejar, utilizando um [configuração desempenho](../app-service-web/web-sites-traffic-manager.md)toosupport sua cobertura de global expandida. Quando os clientes acedem o front-end ou APIs, será encaminhado toohello mais próximo do serviço de aplicações, que por sua vez, irá ligar toohello réplica de base de dados do Cosmos local.

![Plataforma de redes sociais adicionar cobertura global tooyour](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusão
Este artigo tenta tooshed algumas claro para alternativas de Olá de criação de redes sociais completamente no Azure com os serviços de baixo custo e pelo fornecimento de resultados grande através de incentivando Olá de uma distribuição de solução e os dados de múltiplos em camadas de armazenamento denominada "Ladder".

![Diagrama de interação entre os serviços do Azure para redes sociais](./media/social-media-apps/social-media-apps-azure-solution.png)

truth Olá é que não há nenhum marca prata para este tipo de cenários, tem Olá synergy criado pela combinação de Olá dos serviços excelente que nos permitem experiências excelente toobuild: Olá velocidade e a liberdade de base de dados do Azure Cosmos tooprovide uma aplicação excelente de redes social, intelligence Olá atrás de uma solução de pesquisa de primeira classe, como a Azure Search, flexibilidade de Olá de serviços de aplicações do Azure toohost mesmo linguagem aplicações, mas os processos em segundo plano poderosa e Olá expansível Storage do Azure e SQL Database do Azure para armazenar as quantidades enormes de dados e Olá energia análise do Azure Machine Learning toocreate conhecimento e intelligence, que pode fornecer comentários tooour processos e ajude-na fornecem Olá toohello direito conteúdo direita os utilizadores.

## <a name="next-steps"></a>Passos seguintes
toolearn mais sobre casos de utilização para a base de dados do Cosmos, consulte [casos de utilização comuns Cosmos DB](use-cases.md).
