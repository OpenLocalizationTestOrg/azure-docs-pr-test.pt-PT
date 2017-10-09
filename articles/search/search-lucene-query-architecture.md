---
title: arquitetura de motor (Lucene) do aaaFull texto pesquisa na Azure Search | Microsoft Docs
description: "Explicação de Lucene consulta processamento e o documento obtenção conceitos para pesquisa em texto completo, como tooAzure relacionado pesquisa."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Como completa a pesquisa em texto funciona na Azure Search

Este artigo é para os programadores que necessitem de uma compreensão mais aprofundada sobre como funciona a pesquisa em texto completo Lucene na Azure Search. Para consultas de texto, pesquisa do Azure irá fornecer perfeitamente resultados esperados na maioria dos cenários, mas ocasionalmente, poderá obter um resultado que parece "off" preso de algum modo. Nestas situações, a presença de um fundo no Olá quatro fases da execução de consulta Lucene (consultar a análise de análise, lexical, documentar correspondente, a classificação) podem ajudar a identificar os parâmetros de tooquery alterações específico ou de configuração que irá fornecer Olá de índice resultado desejado. 

> [!Note] 
> A pesquisa do Azure utiliza Lucene para pesquisa em texto completo, mas não é exaustiva Lucene integração. Iremos seletivamente expor e expandir Lucene funcionalidade tooenable Olá cenários importante tooAzure pesquisa. 

## <a name="architecture-overview-and-diagram"></a>Descrição geral da arquitetura e diagrama

Processamento de uma consulta de pesquisa de texto completo começa com a análise Olá consulta texto tooextract os termos da procura. o motor de busca Olá utiliza documentos de tooretrieve um índice com termos correspondentes. Termos de consulta individuais, por vezes, são divididos e reconstituted no novo formulários toocast uma rede mais abrangente sobre o que podem ser considerado como uma correspondência potencial. Um conjunto de resultados, em seguida, é ordenado por um relevância pontuação tooeach atribuído individuais correspondente documento. Os, Olá parte superior do Olá classificado lista são devolvidos toohello aplicação de chamada.

Restated, execução de consultas tem quatro fases: 

1. Consulta de análise 
2. Análise lexical 
3. Obtenção de documento 
4. A classificação 

Diagrama de Olá abaixo ilustra Olá componentes utilizados tooprocess um pedido de pesquisa. 

 ![Diagrama de arquitetura de consulta Lucene na Azure Search][1]


| Componentes principais | Descrição funcional | 
|----------------|------------------------|
|**Parsers de consulta** | Separe os termos de consulta de operadores de consulta e crie Olá consulta estrutura (uma árvore de consulta) toobe enviado toohello motor de busca. |
|**Analisadores** | Execute uma análise lexical em termos de consulta. Este processo pode envolver transformar, remover ou de expansão de termos de consulta. |
|**Índice** | Uma estrutura de dados eficiente utilizado toostore e organizar os termos pesquisáveis extraídos de documentos indexados. |
|**Motor de busca** | Obtém e pontuações documentos com base nos conteúdos Olá do índice de Olá inverted de correspondência. |

## <a name="anatomy-of-a-search-request"></a>Anatomy de um pedido de pesquisa

Um pedido de pesquisa é uma especificação de conclua de que deve ser devolvido num conjunto de resultados. A forma mais simples, é uma consulta vazia com sem critérios de qualquer tipo. Um exemplo mais realista inclui parâmetros, muitos outros termos, talvez âmbito toocertain campos, com possivelmente uma expressão de filtro e ordem regras de consulta.  

Olá exemplo seguinte é um pedido de pesquisa poderão enviar tooAzure pesquisa utilizando Olá [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Para este pedido, o motor de busca Olá Olá seguintes:

1. Filtros de saída de documentos onde o preço de Olá é, pelo menos, 60 $ e inferior a 300 $.
2. Executa a consulta de Olá. Neste exemplo, consulta de pesquisa de Olá consiste em expressões e termos: `"Spacious, air-condition* +\"Ocean view\""` (utilizadores, normalmente, não introduzem pontuação, mas permite-na incluir no exemplo de Olá tooexplain como analisadores o processar). Para esta consulta, o motor de busca Olá analisa descrição Olá e campos de título especificado no `searchFields` para documentos que contenham "Vista Ocean" e adicionalmente no prazo de Olá "spacious" ou medida que começa com o prefixo de Olá "air-condition". Olá `searchMode` parâmetro é toomatch utilizado em qualquer termo (predefinição) ou em todos eles, nos casos em que não é necessário explicitamente um termo (`+`).
3. As ordens Olá conjunto resultante dos hotéis por proximidade tooa recebe a localização de geografia e devolvido, em seguida, a aplicação de chamada de toohello. 

Olá maioria deste artigo está sobre o processamento de Olá *consulta de pesquisa*: `"Spacious, air-condition* +\"Ocean view\""`. Filtragem e ordenação estão fora do âmbito. Para obter mais informações, consulte Olá [documentação de referência da API de pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Fase 1: Análise de consulta 

Conforme indicado, cadeia de consulta Olá é a primeira linha de Olá de pedido de Olá: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

consulta Olá parser separa operadores (tais como `*` e `+` no exemplo Olá) a partir de pesquisa de termos e deconstructs consulta de pesquisa de Olá para *subconsultas* de um tipo suportado: 

+ *consulta do termo* termos autónomo (como spacious)
+ *consulta de expressão* termos entre aspas (como ver ocean)
+ *consulta de prefixo* termos seguido de um operador de prefixo `*` (como air-condition)

Para obter uma lista completa dos tipos de consulta suportada consulte [sytnax de consulta Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operadores associados uma subconsulta determinam se a consulta de Olá "tem de ser" ou "deve ser" satisfeito por ordem de um documento toobe considerada uma correspondência. Por exemplo, `+"Ocean view"` é "tem" toohello devida `+` operador. 

o parser de consulta Olá restructures subconsultas Olá para um *árvore de consulta* (uma estrutura interna que representa a consulta de Olá) passa no motor de busca toohello. No Olá primeira fase da consulta de análise, árvore de consulta Olá aspeto.  

 ![Valor booleano consultar searchmode qualquer][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Suportado parsers: simples e Lucene completa 

 A pesquisa do Azure expõe dois idiomas de consulta diferentes, `simple` (predefinição) e `full`. Por definição Olá `queryType` parâmetro com o seu pedido de pesquisa, pode saber parser de consulta Olá o idioma de consulta que escolher, para que o se sabe como toointerpret Olá operadores e sintaxe. Olá [langauge de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) é intuitiva e robusta, muitas vezes adequado toointerpret intervenção do utilizador como-é sem processamento do lado do cliente. Suporta os operadores de consulta familiares web dos motores de busca. Olá [idioma de consulta Lucene completa](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), os quais obtém definindo `queryType=full`, expande o idioma de consulta simples Olá predefinido, adicionando suporte para obter mais operadores e tipos de consulta como caráter universal, difusa, regex e consultas de âmbito de campo. Por exemplo, uma expressão regular enviada na sintaxe de consulta simples seria ser interpretada como uma cadeia de consulta e não uma expressão. pedido de exemplo de Olá neste artigo utiliza o idioma de consulta Lucene completa Olá.

### <a name="impact-of-searchmode-on-hello-parser"></a>Impacto da searchMode no parser de Olá 

Outro parâmetro de pedido de pesquisa que afeta a análise é Olá `searchMode` parâmetro. Controla o operador de predefinição Olá para consultas booleanos: quaisquer (predefinição) ou a totalidade.  

Quando `searchMode=any`, que é a predefinição de Olá, o delimitador de espaço de Olá entre spacious e air-condition ou (`||`), tornando o texto de consulta de exemplo de Olá equivalente ao: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Operadores explícitos, tais como `+` no `+"Ocean view"`, são inequívoca na construção de consultas booleano (termo Olá *tem* corresponder). É menos óbvios como Olá toointerpret restantes termos: spacious e air-condition. Deve motor de busca Olá localizar correspondências na vista de ocean *e* spacious *e* air-condition? Ou deverá encontrar-vista ocean plus *uma* de Olá restantes termos? 

Por predefinição (`searchMode=any`), o motor de busca Olá assume interpretação mais ampla Olá. O campo *deve* corresponder, ao refletir semântica "ou". árvore de consulta inicial Olá anteriormente, ilustrado com Olá duas "deve" operações, mostra Olá predefinido.  

Suponha que definimos agora `searchMode=all`. Neste caso, o espaço de Olá é interpretado como uma operação "and". Cada um dos termos restantes Olá tem estar ambos presente no Olá documento tooqualify como uma correspondência. consulta de exemplo Olá resultante iria devem ser interpretada da seguinte forma: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Uma árvore de modificação da consulta para esta consulta seria o seguinte, em que um documento correspondente é intersecção Olá de todas as três subconsultas: 

 ![Consulta booleano searchmode todos os][3]

> [!Note] 
> Escolher `searchMode=any` através de `searchMode=all` é uma decisão melhor chegou ao executar consultas representativos. Os utilizadores que são tooinclude provável operadores (comum quando documento pesquisa armazena) poderá encontrar resultados mais intuitiva se `searchMode=all` informa construções de consulta booleano. Para mais informações sobre Olá interplay entre `searchMode` e operadores, consulte [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Fase 2: Análise de Lexical 

Processo de analisadores lexical *termo consultas* e *frase consultas* depois de árvore de consulta Olá está estruturada. Um analisador aceita Olá texto entradas fornecidas tooit pelo parser Olá, processos Olá texto e, em seguida, os termos de envia novamente atomizada toobe incorporadas no Olá árvore de consulta. 

Olá formulário mais comuns de análise lexical é *analysis linguístico* que transforma os termos de consulta com base no tooa específico de regras fornecido idioma: 

* Reduzir um formulário de raiz de toohello ao termo de consulta de uma palavra 
* A remover não essencial palavras (palavras de paragem, tais como "a" ou "e" em inglês) 
* Eliminar uma palavra composta em partes de componente 
* Inferior as maiúsculas e minúsculas uma palavra de maiúsculas 

Todas estas operações tendem tooerase diferenças entre a entrada de texto de Olá fornecida pelos termos de utilizador e Olá de Olá armazenados no índice Olá. Operações ponha o processamento de texto e requerem conhecimentos aprofundados de idioma de Olá próprio. tooadd esta camada de sensibilização linguístico, pesquisa do Azure suporta uma longa lista de [analisadores de idioma](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene e Microsoft.

> [!Note]
> Requisitos de análise podem variar entre tooelaborate mínima dependendo do seu cenário. Pode controlar a complexidade da análise lexical ao hello ao selecionar um dos analisadores de Olá predefinida ou criar os seus próprios [analisador personalizado](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analisadores de âmbito toosearchable campos e são especificadas como parte de uma definição de campo. Isto permite-lhe toovary lexical analysis numa base por campo. Não, Olá *padrão* Lucene analisador é utilizado.

No nosso exemplo, tooanalysis anterior, tem de árvore de consulta inicial Olá termo Olá "Spacious", com uma maiúscula "S" e uma vírgula que Olá parser de consulta interpreta como parte do termo de consulta Olá (uma vírgula não é considerada um operador de idioma de consulta).  

Quando o analisador de predefinição Olá processa termo Olá, este será minúsculas de "ocean view" e "spacious" e remover Olá vírgulas caráter. árvore de consulta modificado Olá irão ter o seguinte aspeto: 

 ![Consulta booleana com termos analisados][4]

### <a name="testing-analyzer-behaviors"></a>Comportamentos do analisador de teste 

comportamento de Olá de um analisador pode ser testado usando Olá [analisar API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Forneça o texto Olá que pretende tooanalyze toosee termos de licenciamento que fornecido analisador irá gerar. Por exemplo, toosee como analisador padrão Olá seria processar Olá texto "air-condition", pode emitir Olá pedido os seguintes:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

Analisador de padrão Olá quebras de texto de entrada Olá para Olá seguir dois tokens, anotá-los com os atributos como iniciar e desvios de fim (utilizados para acessos realce), bem como a respetiva posição (utilizado para a correspondência de expressão):

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Análise de toolexical de exceções 

Análise lexical aplica-se apenas os tipos de tooquery que requerem concluídos termos – uma consulta do prazo ou uma consulta de expressão. Se não aplica tooquery tipos com os termos incompletos – consulta de prefixo, consulta de caráter universal, consulta regex – ou consulta difusa tooa. Os tipos, incluindo a consulta de prefixo de Olá com o termo de consulta *air-condition\**  no nosso exemplo, são adicionados diretamente da árvore de consulta toohello, ignorando a fase de análise Olá. Olá apenas efetuada em termos de consulta desses tipos de transformação é lowercasing.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Fase 3: Obtenção de documento 

Obtenção de documento refere-se toofinding documentos com termos correspondentes no índice Olá. Nesta fase é compreendida melhor através de um exemplo. Vamos começar com um índice de hotéis ter Olá seguir esquema simple: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Mais partem do princípio de que este índice contém Olá quatro documentos que os seguintes: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Como são indexados termos**

obtenção toounderstand, ajuda a tooknow algumas noções básicas sobre a indexação. unidade de Olá de armazenamento é um índice inverted, um para cada campo pesquisável. Dentro de um índice inverted é uma lista ordenada de todos os termos de todos os documentos. Cada termo mapeia toohello lista de documentos em que ocorrer, como evidente no exemplo Olá abaixo.

termos de Olá tooproduce num índice inverted, motor de busca Olá efetua a análise lexical sobre conteúdo Olá de documentos, toowhat semelhante ocorre durante o processamento de consulta. Entradas de texto são transmitidas tooan analyzer, cased inferior repartidas de pontuação e assim sucessivamente, consoante a configuração do analisador de Olá. É comum, mas não é necessária, toouse Olá mesmos analisadores de pesquisa e indexação operações, para que os termos de consulta parecer mais como termos dentro Olá índice.

> [!Note]
> A pesquisa do Azure permite-lhe especificar diferentes analisadores de indexação e procurar através de adicionais `indexAnalyzer` e `searchAnalyzer` parâmetros de campo. Se não for indicado, Olá analisador definida com Olá `analyzer` propriedade é utilizada para indexação e pesquisa.  

**Inverted índice para documentos de exemplo**

Devolver o exemplo de tooour, para Olá **título** campo, índice Olá inverted tem este aspeto:

| Termo | Lista de documentos |
|------|---------------|
| atman | 1 |
| Beach | 2 |
| átrios | 1, 3 |
| Ocean | 4  |
| playa | 3 |
| recurso | 3 |
| Retreat | 4 |

Olá título campo, apenas *átrios* aparece em dois documentos: 1, 3.

Para Olá **Descrição** campo, índice Olá é o seguinte:

| Termo | Lista de documentos |
|------|---------------|
| ar | 3
| e | 4
| Beach | 1
| ter | 3
| -Se confortáveis ao | 3
| Distância | 1
| Ilha | 2
| kauaʻi | 2
| localizado | 2
| Norte | 2
| Ocean | 1, 2, 3
| de | 2
| no |2
| silenciosos | 4
| gabinetes  | 1, 3
| secluded | 4
| shore | 2
| spacious | 1
| Olá | 1, 2
| demasiado| 1
| ver | 1, 2, 3
| walking | 1
| com o | 3


**Termos de consulta correspondente contra indexados termos**

Tendo em conta os índices de Olá inverted acima, vamos voltar a consulta de exemplo toohello e ver documentos correspondentes como encontram-se para a nossa consulta de exemplo. Recuperar que nessa árvore de consulta final Olá tem o seguinte aspeto: 

 ![Consulta booleana com termos analisados][4]

Durante a execução de consulta, consultas individuais são executadas em relação a campos pesquisáveis Olá independentemente. 

+ Olá TermQuery, "spacious" corresponde ao documento 1 (átrios Atman). 

+ Olá PrefixQuery, "air-condition *", não corresponde a quaisquer documentos. 

  Este é um comportamento que confuses, por vezes, os programadores. Embora o termo Olá air-conditioned existe no documento de Olá, é dividida em dois termos pelo analisador do Olá predefinido. Recuperar-se de que as consultas de prefixo, que contêm termos parciais, não são analisadas. Por conseguinte termos com o prefixo "air-condition" é pesquisado em Olá inverted índice e não foi encontrado.

+ Olá PhraseQuery, "vista ocean", procura Olá termos "ocean" e "ver" e verifica proximidade Olá dos termos de documento original Olá. Documentos 1, 2 e 3 correspondem a esta consulta no campo de descrição de Olá. Documento de aviso 4 tem ocean do termo Olá no título de Olá, mas não é considerado uma correspondência, como podemos está à procura de expressão de "ocean view" Olá, em vez de palavras individuais. 

> [!Note]
> Uma consulta de pesquisa é executada de forma independente em relação a todos os campos pesquisáveis no Olá de índice da Azure Search a menos que limite os campos de Olá definida com Olá `searchFields` parâmetro, conforme ilustrado no pedido de pesquisa de exemplo de Olá. Documentos que correspondam em qualquer um dos campos de Olá selecionado, são devolvidos. 

Olá todo, para a consulta de Olá em questão, documentos Olá correspondentes são 1, 2, 3. 

## <a name="stage-4-scoring"></a>Testar 4: classificação  

Todos os documentos de um conjunto de resultados de pesquisa é atribuído uma pontuação de importância. função de Olá de pontuação de relevância Olá é superior esses documentos que melhor responder a um utilizador pergunta, expressa pelo consulta de pesquisa de Olá toorank. pontuação Olá é calculada com base nas propriedades de análises de termos correspondentes. Olá núcleos de Olá classificação fórmula está [TF/IDF (frequência de documento de frequência inverso termo)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). Em consultas que contém termos raros e comuns, TF/IDF promove resultados que contém o termo raro Olá. Por exemplo, um índice hipotético com todos os artigos Wikipedia, de documentos que consulta Olá correspondentes *president Olá*, documentos correspondente no *president* são consideradas mais relevante que documentos correspondente no *o*.


### <a name="scoring-example"></a>A classificação de exemplo

Recuperar os documentos de três Olá que correspondeu à nossa consulta de exemplo:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

O documento 1 consulta Olá correspondentes melhor porque ambos Olá termo *spacious* e o frase necessário Olá *vista ocean* ocorrer no campo de descrição de Olá. Olá junto dois documentos corresponde à frase de Olá apenas *vista ocean*. Poderá ser surprising esse pontuação de relevância Olá para documento 2 e 3 é diferente, apesar de estes corresponde à consulta Olá Olá mesma forma. É porque Olá classificação fórmula tem mais componentes que acabou de TF/IDF. Neste caso, o documento 3 foi atribuído uma pontuação ligeiramente porque a respetiva descrição é mais pequeno. Saiba mais sobre [práticas da classificação de fórmula do Lucene](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand como o comprimento do campo e ainda outros fatores podem influenciar Olá pontuação de importância.

Alguns tipos (universal, prefixo, regex) de consulta contribuir sempre uma pontuação constante toohello geral pontuação de documentos. Isto permite correspondências encontradas através da consulta expansão toobe incluída nos resultados de Olá, mas sem afetar a classificação de Olá. 

Um exemplo ilustra a razão pela qual isto é importante. Pesquisas com carateres universais, incluindo as pesquisas de prefixo, são ambíguas pela definição porque a entrada de Olá é uma cadeia parcial com potenciais correspondências num número muito grande de diferentes termos (considere uma entrada de "apresentação *", com correspondências encontradas "tours", "tourettes", e " tourmaline"). Tendo em conta natureza Olá estes resultados, não há nenhuma forma tooreasonably inferir os termos encontram-se mais importantes do que outros. Por este motivo, estamos a ignorar frequências termo quando a classificação de resultados em consultas de caráter universal de tipos, o prefixo e o regex. Num pedido de várias partes de pesquisa que inclui termos parciais e integrais, resultados de entrada parcial Olá são incorporados com uma constante tooavoid bias para correspondências potencialmente inesperadas de pontuação.

### <a name="score-tuning"></a>Otimização de pontuação

Existem duas formas pontuações de relevância tootune na pesquisa do Azure:

1. **Perfis de classificação** promover documentos na lista de Olá classificado de resultados com base num conjunto de regras. No nosso exemplo, podemos considerar documentos correspondentes no campo do título de Olá mais relevante que documentos correspondentes no campo de descrição de Olá. Além disso, se o nosso índice tinha um campo de preço para cada átrios, iremos promover documentos com preço inferior. Mais informações sobre como demasiado[adicionar o índice de pesquisa de tooa de perfis de classificação.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Termo aumento** (disponível apenas no Olá completa consulta lucene) fornece um operador de aumento `^` que podem ser aplicadas tooany parte da árvore de consulta Olá. No nosso exemplo, em vez de procurar no prefixo de Olá *air-condition*\*, um pode procurar um termo exato de Olá *air-condition* ou prefixo Olá, mas os documentos que corresponda a Olá exato termo estão ordenadas superior aplicando a consulta do aumento toohello termo: *ondas condição ^ 2 | | Air-condition**. Saiba mais sobre [termo aumento](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Classificação de um índice distribuído

Todos os índices na pesquisa do Azure são automaticamente dividido em várias shards, permitindo-nos tooquickly distribuir índice Olá entre vários nós durante a escala do serviço de segurança ou reduzir verticalmente. Quando é emitido um pedido de pesquisa, este é emitido em relação a cada partição horizontal independentemente. Olá resultados de cada ID de partição horizontal são, em seguida, intercalar e ordenados pelo modelo de pontuação (se não existem outros ordenação está definido). É importante tooknow que Olá classificação função ponderações consulta termo frequência contra a frequência de documento inverso em todos os documentos no ID de partição horizontal Olá, não em todas as partições horizontais!

Isto significa uma pontuação de relevância *foi* ser diferentes para documentos idênticos se que residem no shards diferentes. Felizmente, estas diferenças tendem toodisappear à medida que cresce número Olá de documentos no índice Olá devido a distribuição de termo mesmo toomore. Não é possível tooassume no qual partições horizontais qualquer documento fornecido será efetuado. No entanto, partindo do princípio de uma chave de documento não irá alterar, este será sempre atribuído toohello mesmo partições horizontais.

Em geral, pontuação de documento não é atributo melhor de Olá para ordenação documentos se estabilidade ordem é importante. Por exemplo, tendo em conta documento duas com uma pontuação idêntico, não há nenhuma garantia que aparece primeiro na execuções subsequentes do Olá mesma consulta. Pontuação de documento deve apenas dar um sentido geral de relevância documento tooother relativo documentos no conjunto de resultados de Olá.

## <a name="conclusion"></a>Conclusão

Olá com êxito de motores de busca internet gerou expetativas para pesquisa em texto completo sobre dados privados. Para praticamente todos os tipos de experiência de pesquisa, agora Esperamos Olá motor toounderstand nossa intenção, mesmo quando os termos estão mal escritos ou está incompleta. Esperamos poderá mesmo correspondências com base nas quase equivalentes termos ou sinónimos que nunca, na verdade, especificamos.

A partir de um ponto de vista técnico, pesquisa em texto completo é altamente complexa, exigindo que uma análise sofisticada linguístico e tooprocessing uma abordagem systematic de formas que distill, expanda e transformar consulta termos toodeliver um resultado relevante. Tendo em conta complexidades inerente Olá, existem muitos fatores que podem afetar o resultado de Olá de uma consulta. Por este motivo, investir mechanics do Olá tempo toounderstand Olá de pesquisa em texto completo oferece vantagens tangible quando tenta toowork através de resultados inesperados.  

Este artigo explorou a pesquisa em texto completo no contexto de Olá da Azure Search. Esperamos que dá-lhe suficientes em segundo plano toorecognize possíveis causas e soluções para problemas comuns de consulta de endereçamento. 

## <a name="next-steps"></a>Passos seguintes

+ Criar o índice de exemplo de Olá, experimentar diferentes consultas e reveja os resultados. Para obter instruções, consulte [compilar e consultar um índice no portal de Olá](search-get-started-portal.md#query-index).

+ Tente sintaxe de consulta adicionais de Olá [documentos sobre pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) secção de exemplo ou a partir de [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) no Explorador de pesquisa no portal de Olá.

+ Reveja [classificação perfis](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) se quiser tootune classificação na sua aplicação de pesquisa.

+ Saiba como tooapply [analisadores de lexical específicas do idioma](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configurar analisadores personalizados](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) para processamento mínimo ou processamento especializado em campos específicos.

+ [Comparar analisadores de padrão e inglês](http://alice.unearth.ai/)) do lado do lado a lado neste web site de demonstração. 

## <a name="see-also"></a>Consultar também

[API de REST de documentos de pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Total de consulta lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Processar os resultados da pesquisa](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
