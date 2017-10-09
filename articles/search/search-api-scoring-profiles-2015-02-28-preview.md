---
title: "perfis de aaaScoring (Azure pesquisa REST API versão 2015-02-28-pré-visualização) | Microsoft Docs"
description: "A pesquisa do Azure é um serviço de pesquisa de nuvem alojada que suporte a otimização de resultados classificados com base nos perfis de classificação definida pelo utilizador."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Perfis de classificação (pesquisa do Azure REST API versão 2015-02-28-pré-visualização)
> [!NOTE]
> Este artigo descreve os perfis de classificação Olá [pré-visualização 2015-02-28](search-api-2015-02-28-preview.md). Atualmente não há qualquer diferença entre Olá `2016-09-01` versão documentadas na [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) e Olá `2015-02-28-Preview` versão descrito aqui, mas que oferecemos neste documento mesmo assim na cobertura de documento ordem tooprovide em Olá API de todo.
>
>

## <a name="overview"></a>Descrição geral
Classificação refere-se de toohello o cálculo de pontuação de pesquisa para cada item devolvido nos resultados da pesquisa. pontuação Olá é um indicador de relevância de um item no contexto de Olá da operação de pesquisa atual Olá. pontuação de Olá superior Olá, Olá mais relevante Olá item. Nos resultados de pesquisa, os itens estão ordenada do toolow elevada, com base no Olá pontuação de pesquisa calculadas para cada item de classificação.

A pesquisa do Azure utiliza a classificação toocompute uma pontuação inicial, mas pode personalizar o cálculo de Olá através de um perfil de classificação. Perfis de classificação dão-lhe maior controlo sobre a classificação de Olá dos itens nos resultados da pesquisa. Por exemplo, poderá pretender itens tooboost com base na respetiva receitas potenciais, promover itens mais recentes ou talvez melhorar itens que foram no inventário demasiado longo.

Um perfil de classificação faz parte da definição do índice Olá, composta por campos, funções e os parâmetros.

toogive tem uma ideia de um perfil de classificação aparência, hello exemplo seguinte mostra um perfil simple com o nome 'georreplicação'. Este boosts itens que tenham o termo de pesquisa de Olá no Olá `hotelName` campo. Também utiliza Olá `distance` toofavor itens que estão dentro do kilometers dez da localização atual Olá de função. Se alguém procura no prazo de Olá 'inn' e 'inn' acontece toobe parte do nome de átrios Olá, documentos que incluem hotéis com 'inn' serão apresentada nos resultados de pesquisa de Olá superiores.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse que este perfil de classificação, a consulta é formulated perfil de Olá toospecify na cadeia de consulta Olá. Consulta de Olá abaixo, tenha em atenção o parâmetro de consulta Olá, `scoringProfile=geo` no pedido de Olá.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Esta consulta pesquisa o termo Olá 'inn' e transmite na localização atual Olá. Tenha em atenção que esta consulta inclui outros parâmetros, tais como `scoringParameter`. Parâmetros de consulta descritos [documentos sobre pesquisa (API da Azure Search)](search-api-2015-02-28-preview.md#SearchDocs).

Clique em [exemplo](#example) tooreview um exemplo mais detalhado de um perfil de classificação.

## <a name="what-is-default-scoring"></a>O que é a classificação de predefinição?
Classificação calcula uma pontuação de pesquisa para cada item num conjunto de resultados ordenada classificação. Todos os itens de um conjunto de resultados de pesquisa é atribuído uma pontuação de pesquisa, em seguida, classificado toolowest mais elevado. Os itens com pontuações superiores Olá são devolvidos toohello aplicação. Por predefinição, hello 50 superior são devolvidos, mas pode utilizar Olá `$top` parâmetro tooreturn um número inferior ou superior de itens (cópia de segurança too1000 numa única resposta).

Por predefinição, uma pontuação de pesquisa é calculada com base nas propriedades de análises de dados de Olá e consulta de Olá. A pesquisa do Azure encontra documentos que incluem os termos da procura Olá na cadeia de consulta Olá (alguns ou todos os, dependendo das `searchMode`), favoring documentos que contenham várias instâncias do termo de pesquisa de Olá. pontuação de pesquisa de Olá passa cópias de segurança superior, mesmo se termo Olá é raro em corpus de dados de Olá, mas comuns no documento de Olá. base de Olá para relevância de toocomputing esta abordagem é conhecido como TF-IDF ou (frequência de documento de frequência inverso termo).

Resultados pressupondo que não há qualquer ordenação personalizado, são, em seguida, ordenados pelo pontuação de pesquisa antes de poderem ser devolvidas toohello aplicação de chamada. Se `$top` não for especificado, 50 itens ter pesquisa mais elevada de Olá pontuação é devolvidas.

Os valores de pontuação de pesquisa podem ser repetidos ao longo de um conjunto de resultados. Por exemplo, poderá ter 10 itens com uma pontuação de 1.2, 20 itens com uma pontuação de 1.0 e 20 itens com uma pontuação de 0,5. Quando vários pedidos ter hello mesmo pontuação de pesquisa, Olá ordenação dos itens classificadas mesmos não está definido e não está estável. Executar novamente a consulta de Olá e poderá ver itens deslocar posição. Tendo em conta dois itens com uma pontuação idêntica, não há nenhuma garantia que aparece em primeiro lugar.

## <a name="when-toouse-custom-scoring"></a>Quando toouse da classificação personalizada
Deve criar um ou mais perfis de classificação quando predefinido Olá classificação comportamento não aceda suficiente na cumprir os objetivos de negócio. Por exemplo, poderá decidir que procura relevância deve favor itens adicionados recentemente. Da mesma forma, poderá ter um campo que contém a margem de lucros ou algum outro campo que indicam potenciais de receitas. Os aumentos pedidos colocar benefícios comerciais tooyour podem ser um fator importante decidir toouse perfis de classificação.

Com base em relevancy ordenação também é implementado através da classificação de perfis. Considere os resultados da pesquisa páginas utilizou Olá anterior que permitem ordenar por preço, data, classificação ou relevância. Na Azure Search, perfis de classificação unidade opção do Olá 'relevância'. definição de Olá de relevância é controlada por si, predicated nos objetivos de negócio e o tipo de Olá de experiência de pesquisa que pretende toodeliver.

<a name="example"></a>

## <a name="example"></a>Exemplo
Conforme indicado, classificação personalizada é implementada através de perfis definidos no esquema de índice de classificação.

Este exemplo mostra Olá esquema de um índice com dois perfis de classificação (`boostGenre`, `newAndHighlyRated`). Qualquer consulta em relação a este índice que inclui o perfil, como um parâmetro de consulta irá utilizar o conjunto de resultados do Olá perfil tooscore Olá.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Fluxo de trabalho
tooimplement personalizada da classificação de comportamento, adicione um esquema de toohello classificação de perfil que define o índice de Olá. Pode fazer cópias de segurança dos perfis de classificação too16 dentro de um índice (consulte [limites de serviço](search-limits-quotas-capacity.md)), mas só pode especificar um perfil de momento, em qualquer consulta especificada.

Começar a utilizar Olá [modelo](#bkmk_template) fornecidas neste tópico.

Forneça um nome. Perfis de classificação são opcionais, mas se adicionar um, é necessário o nome de Olá. Ser toofollow se as convenções de nomenclatura Olá para campos (começa com uma letra, evita carateres especiais e palavras reservadas). Consulte [regras de nomenclatura](http://msdn.microsoft.com/library/azure/dn857353.aspx) para obter mais informações.

corpo de Olá do perfil de classificação de Olá é construído a partir de ponderado campos e funções.

### <a name="weights"></a>Ponderações
Olá `weights` pares nome-valor que atribuir um campo de tooa peso relativo de Especifica a propriedade de um perfil de classificação. No Olá [exemplo](#example), Olá albumTitle, género, artistName campos e são elevada 1.5, 5 e 2, respetivamente. Por que motivo é género elevado, por isso, muito superior do que outras pessoas Olá? Se a procura é efetuada através de dados que são um pouco homogénea (como é Olá caso com género no Olá `musicstoreindex`), poderá ter uma maior variância em ponderações relativo Olá. Por exemplo, no Olá `musicstoreindex`, 'rock' aparece como ambos um género e nas descrições de forma idêntica phrased género. Se pretender que a descrição do género toooutweigh género, o campo do género de Olá terá um muito peso relativo superior.

### <a name="functions"></a>Funções
As funções são utilizadas quando cálculos adicionais são necessários para contextos específicos. Os tipos de função válido são `freshness`, `magnitude`, `distance` e `tag`. Cada função tem parâmetros que são tooit exclusivo.

* `freshness`deve ser utilizado quando quiser tooboost pelo novo ou antigo como um item é. Esta função só pode ser utilizada com os campos datetime (`Edm.DataTimeOffset`). Olá nota `boostingDuration` atributo é utilizado apenas com a função de reatualização Olá.
* `magnitude`deve ser utilizado quando quiser é tooboost com base na forma como elevado ou baixo um valor numérico. Os cenários que chamam para esta função incluem os aumentos por margem de lucros, preços mais elevado, preços mais baixo ou um número de transferências. É possível inverter intervalo Olá, toolow elevada, se pretender que o padrão de inverso Olá (por exemplo, tooboost um preço inferior itens mais do que um preço superior itens). Fornecido um intervalo de preços de $100 demasiado$ 1, deverá definir `boostingRangeStart` em 100 e `boostingRangeEnd` em itens de um preço inferior Olá de 1 tooboost. Esta função só pode ser utilizada com campos de valor de duplo e o número inteiro.
* `distance`deve ser utilizada quando quiser tooboost por proximidade ou localização geográfica. Esta função só pode ser utilizada com `Edm.GeographyPoint` campos.
* `tag`deve ser utilizado quando quiser tooboost por etiquetas em comum entre documentos e consultas de pesquisa. Esta função só pode ser utilizada com `Edm.String` e `Collection(Edm.String)` campos.

#### <a name="rules-for-using-functions"></a>Regras para a utilização de funções
* Tipo de função (reatualização magnitude, distância, tag) tem de ser minúsculas.
* As funções não podem incluir valores nulos nem vazios. Especificamente, se incluir fieldname, terá de tooset-toosomething.
* As funções só podem ser aplicados toofilterable campos. Consulte [Create Index](search-api-2015-02-28-preview.md#CreateIndex) para obter mais informações sobre campos filtráveis.
* As funções só podem ser aplicados toofields que estão definidos na coleção de campos de Olá de um índice.

Depois de índice de Olá estiver definido, crie índice Olá ao carregar o esquema de índice Olá, seguido de documentos. Consulte [Create Index](search-api-2015-02-28-preview.md#CreateIndex) e [adicionar ou atualizar documentos](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) para obter instruções sobre estas operações. Uma vez que é criado o índice de Olá, deve ter um perfil de classificação funcional que funciona com os seus dados de pesquisa.

<a name="bkmk_template"></a>

## <a name="template"></a>Modelo
Esta secção mostra a sintaxe de Olá e o modelo para perfis de classificação. Consulte demasiado[referência do atributo de índice](#bkmk_indexref) na secção seguinte, Olá para obter descrições de atributos de Olá.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Referência da propriedade de perfil de classificação
> [!NOTE]
> Uma função de classificação só pode ser aplicados toofields que são filtrável.
>
>

| Propriedade | Descrição |
| --- | --- |
| `name` |Necessário. Este é o nome de Olá de Olá perfil de classificação. -Forma Olá mesmas convenções de nomenclatura de um campo. -Tem de começar com uma letra, não pode conter pontos, vírgula ou @ símbolos e não pode começar com o frase Olá "azuresearch, uma vez" (maiúsculas e minúsculas). |
| `text` |Contém a propriedade de ponderações Olá. |
| `weights` |Opcional. Um par nome / valor que especifica um nome de campo e o peso relativo. Peso relativo tem de ser um número inteiro positivo ou o número de vírgula flutuante. Pode especificar o nome do campo Olá sem uma ponderação correspondente. Ponderações são utilizados tooindicate Olá importância de tooanother relativo de um campo. |
| `functions` |Opcional. Tenha em atenção que uma função de classificação só pode ser aplicados toofields que são filtrável. |
| `type` |Necessário para funções de classificação. Indica o tipo de Olá de toouse de função. Os valores válidos incluem `magnitude`, `freshness`, `distance` e `tag`. Pode incluir mais de uma função em cada perfil de classificação. o nome de função Olá tem de ser minúsculas. |
| `boost` |Necessário para funções de classificação. Um número positivo utilizado como multiplicador para a classificação não processada. Não pode ser too1 igual. |
| `fieldName` |Necessário para funções de classificação. Uma função de classificação só pode ser aplicados toofields que fazem parte da coleção de campo Olá do índice de Olá e que são filtrável. Além disso, cada tipo de função apresenta as restrições adicionais (reatualização é utilizada com os campos datetime, magnitude com um número inteiro ou duplo campos, distância com campos de localização e etiqueta com a cadeia ou campos de coleção de cadeia). Só é possível especificar um único campo por definição de função. Para o exemplo, toouse magnitude duas vezes em Olá mesmo perfil, terá de magnitude de definições de tooinclude dois, um para cada campo. |
| `interpolation` |Necessário para funções de classificação. Define o declive Olá para a classificação que Olá os aumentos aumentam desde início Olá Olá toohello final do intervalo de Olá. Os valores válidos incluem `linear` (predefinição), `constant`, `quadratic`, e `logarithmic`. Consulte [definir interpolations](#bkmk_interpolation) para obter mais detalhes. |
| `magnitude` |função de pontuação de magnitude de Olá é as classificações de tooalter utilizados com base no intervalo de Olá de valores de um campo numérico. Alguns exemplos de mais comuns utilização Olá deste são:<ul><li>Classificações em estrelas: Alter Olá classificação com base no valor de Olá no campo "Estrela de classificação" Olá. Quando dois itens são relevantes, item de Olá com a classificação superior Olá apresentada pela primeira vez.</li><li>A margem: Quando dois documentos são relevantes, um revendedor poderá desejar tooboost documentos que tenham as margens superiores pela primeira vez.</li><li>Clique em contagens: para aplicações que controlam clique através de ações tooproducts ou páginas, pode utilizar itens de tooboost de magnitude tendem tooget Olá maioria do tráfego.</li><li>Transferir contagens: para aplicações que controlam as transferências, Olá magnitude função permite melhorar itens que tenham Olá a maioria das transferências.</li></ul> |
| `magnitude:boostingRangeStart` |Olá conjuntos iniciar o valor do intervalo de Olá durante o qual é classificada a magnitude. valor de Olá tem de ser um número inteiro ou o número de vírgula flutuante. Para classificações em estrelas de 1 a 4, isto seria 1. Para margens superiores a 50%, isto seria 50. |
| `magnitude:boostingRangeEnd` |Define o valor de fim de Olá do intervalo de Olá durante o qual é classificada a magnitude. valor de Olá tem de ser um número inteiro ou o número de vírgula flutuante. Para classificações em estrelas de 1 a 4, isto seria 4. |
| `magnitude:constantBoostBeyondRange` |Os valores válidos são VERDADEIRO ou FALSO (predefinição). Quando definida tootrue, aumento total Olá continuará toodocuments tooapply que tenham um valor para o campo de destino Olá que seja superior ao mais Olá superior do intervalo de Olá. Se for FALSO, a intensificação desta função Olá será aplicado toodocuments que tenham um valor para o campo de destino Olá que esteja fora do intervalo de Olá. |
| `freshness` |a função de classificação de atualização de Olá é utilizado tooalter classificação pontuações das classificações para itens com base em valores nos campos DateTimeOffset. Por exemplo, um item com uma data mais recente pode ser ordenado superior do que os itens mais antigos. (Tenha em atenção que também é possível toorank itens, como eventos de calendário com datas futuras que itens toohello próximo presente pode classificar superior mais itens na Olá futura.) A versão de serviço atual Olá, um fim do intervalo de Olá irá ser corrigido toohello hora atual. Olá outra extremidade é uma hora no Olá passado com base no Olá `boostingDuration`. tooboost um intervalo de horas no Olá futura utilizar negativo `boostingDuration`. taxa de Olá no qual Olá os aumentos alterações a partir de um intervalo mínimo e máximo é determinado pelo Olá interpolação aplicada toohello perfil de classificação (consulte a figura Olá abaixo). tooreverse Olá fator aumento aplicada, escolha um fator de aumento de menor que 1. |
| `freshness:boostingDuration` |Define um período de expiração após o qual os aumentos param para um documento em particular. Consulte [definir boostingDuration](#bkmk_boostdur) no Olá secção para a sintaxe e exemplos a seguir. |
| `distance` |distância Olá da classificação de função é Olá tooaffect utilizados pontuação dos documentos com base na fechar ou até que ponto são localização geográfica de referência tooa relativo. localização de referência de Olá é fornecida como parte da consulta de Olá num parâmetro (utilizando Olá `scoringParameter` parâmetro de consulta) como um lon, lat argumento. |
| `distance:referencePointParameter` |Toobe um parâmetro transmitido consultas toouse como localização de referência. scoringParameter é um parâmetro de consulta. Consulte [documentos sobre pesquisa](search-api-2015-02-28-preview.md#SearchDocs) para obter descrições de parâmetros de consulta. |
| `distance:boostingDistance` |Um número que indica a distância Olá em quilómetros, da localização de referência de olá onde Olá os aumentos intervalo termina. |
| `tag` |Olá tag de classificação de função é utilizada pontuação de Olá tooaffect dos documentos com base nas etiquetas em documentos e consultas de pesquisa. Documentos que tenham etiquetas in common with consulta de pesquisa de Olá irão ser elevados. Olá etiquetas para consulta de pesquisa de Olá é fornecida como um parâmetro de classificação em cada pedido de pesquisa (utilizando Olá `scoringParameter` parâmetro de consulta). |
| `tag:tagsParameter` |Toobe um parâmetro transmitido nas consultas toospecify etiquetas para um pedido específico. `scoringParameter`é um parâmetro de consulta. Consulte [documentos sobre pesquisa](search-api-2015-02-28-preview.md#SearchDocs) para obter descrições de parâmetros de consulta. |
| `functionAggregation` |Opcional. Aplica-se apenas quando as funções são especificadas. Os valores válidos incluem: `sum` (predefinição), `average`, `minimum`, `maximum`, e `firstMatching`. Uma pontuação de pesquisa é um valor único, que é calculado a partir de várias variáveis, incluindo várias funções. Este atributos indica como boosts Olá de todas as funções de Olá são combinados necessita de uma único agregada aumento que é então aplicado toohello base pontuação de documento. pontuação base Olá baseia-se no valor de tf-idf Olá calculado a partir do documento Olá e consulta de pesquisa de Olá. |
| `defaultScoringProfile` |Quando executar um pedido de pesquisa, não se for especificado nenhum perfil de classificação, em seguida, predefinidas de classificação é utilizada (tf-idf apenas). Uma predefinição de nome do perfil de classificação pode ser definida aqui, fazendo com que da Azure Search toouse esse perfil quando nenhum perfil específico é dado em pedido de pesquisa de Olá. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Conjunto interpolations
Interpolations permitem-lhe declive de Olá toodefine para a classificação que Olá os aumentos aumentam desde início Olá Olá toohello final do intervalo de Olá. pode ser utilizado Olá interpolations os seguintes:

* `Linear`: Para itens que se encontrem dentro de Olá máximo e mínimo intervalo, Olá intensificação aplicada toohello item será efetuada num período constantemente diminuir. Linear é interpolação de predefinição Olá para um perfil de classificação.
* `Constant`: Para itens que se encontrem dentro de Olá inicial e final do intervalo, um aumento constante será aplicado toohello resultados de classificação.
* `Quadratic`: Na comparação tooa interpolação Linear que tenha um aumento constantemente diminuir, Quadratic inicialmente irá diminuir ao ritmo mais pequeno e, em seguida, como os se aproxima intervalo de fim de Olá,-diminui num intervalo muito superior. Esta opção de interpolação não é permitida numa tag da classificação de funções.
* `Logarithmic`: Na comparação tooa interpolação Linear que tenha um aumento constantemente diminuir, Logarithmic inicialmente irá diminuir ao ritmo superior e, em seguida, como os se aproxima intervalo de fim de Olá,-diminui num intervalo muito menor. Esta opção de interpolação não é permitida numa tag da classificação de funções.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Conjunto boostingDuration
`boostingDuration`é um atributo da função de reatualização Olá. Pode utilizá-lo tooset um período de expiração após o qual os aumentos param para um documento em particular. Por exemplo, tooboost uma linha de produto ou marca durante um período de promocional de 10 dias, tem de especificar período de 10 dias Olá como "P10D" para esses documentos. Ou especifique tooboost futuros eventos Olá próximas semanas "-P7D".

`boostingDuration`tem de ser formatado como um valor de "dayTimeDuration" XSD (um subconjunto restrito de um valor de duração ISO 8601). Olá padrão para isto é: `[-]P[nD][T[nH][nM][nS]]`.

Olá, a tabela seguinte fornece vários exemplos.

| Duração | boostingDuration |
| --- | --- |
| 1 dia |"P1D" |
| 2 dias e 12 horas |"P2DT12H" |
| 15 minutos |"PT15M" |
| 30 dias, 5 horas, 10 minutos, e 6.334 segundos |"P30DT5H10M6.334S" |

Para obter mais exemplos, consulte [esquema XML: tipos de dados (W3.org web site)](http://www.w3.org/TR/xmlschema11-2/).

**Consulte também**
[API de REST do serviço de pesquisa do Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN <br/>
[Criar índice (pesquisa do Azure API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) no MSDN<br/>
[Adicione um índice de pesquisa de tooa perfil classificação](http://msdn.microsoft.com/library/azure/dn798928.aspx) no MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
