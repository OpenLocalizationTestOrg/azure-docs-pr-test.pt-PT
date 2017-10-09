---
title: "APIs do Machine Learning: Análise de texto | Microsoft Docs"
description: "APIs de análise de texto de aprendizagem máquina da Microsoft podem ser utilizado tooanalyze texto não estruturado para análise de dados de sentimento, extração de expressão de chave, deteção de idioma e deteção de tópico."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>APIs de Machine Learning: Análise de Texto para Sentimentos, Extração de Expressões-Chave, Deteção de Idioma e Deteção de Tópicos
> [!NOTE]
> Este guia destina-se a versão 1 do Olá API. Para a versão 2, [ **Consulte toothis documento**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versão 2 está agora versão preferencial de Olá desta API.
> 
> 

## <a name="overview"></a>Descrição geral
Olá API de análise de texto é um conjunto de análise de texto [serviços web](https://datamarket.azure.com/dataset/amla/text-analytics) criadas com o Azure Machine Learning. Olá API pode ser utilizado tooanalyze texto não estruturado para tarefas como a análise de dados de sentimento, extração de expressão de chave, deteção de idioma e deteção de tópico. Não são de dados de formação necessário toouse esta API: apenas colocar os dados de texto. Esta API utiliza avançada linguagem natural processamento técnicas toodeliver melhor no predições de classe.

Pode ver análise de texto em ação na nossa [site demonstração](https://text-analytics-demo.azurewebsites.net/), onde também encontrará [amostras](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sobre como tooimplement análise de texto em c# e Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Análise de sentimentos
Olá API devolve uma pontuação numérico entre 0 e 1. Too1 fechar pontuações indicar sentimento positivo, enquanto too0 fechar pontuações indicar sentimento negativo. A pontuação do sentimento é gerada através de técnicas de classificação. Olá funcionalidades entrada toohello classificador incluem n-grams, geradas a partir de etiquetas de parte de voz e o word embeddings de funcionalidades. Atualmente, o inglês é Olá idioma suportado apenas.

## <a name="key-phrase-extraction"></a>Extração de expressões chave
Olá API devolve uma lista de cadeias que indica Olá chave talking pontos de texto de entrada Olá. Utilizamos técnicas do toolkit de Processamento de Linguagens Naturais do Microsoft Office. Atualmente, o inglês é Olá idioma suportado apenas.

## <a name="language-detection"></a>Deteção de idioma
Olá API devolve Olá detetou linguagem e uma pontuação numérico entre 0 e 1. Too1 fechar pontuações indicar certainty 100% se idioma Olá identificado é verdadeiro. É suportado um total de 120 idiomas.

## <a name="topic-detection"></a>Deteção de tópicos
Esta é uma API recentemente publicada que devolve Olá principais tópicos detetado para obter uma lista de registos de texto foi submetido. É identificado um tópico com uma expressão chave, a qual pode ser constituída por uma ou mais palavras relacionadas. Esta API requer um mínimo de texto 100 regista toobe submetido, mas é concebida toodetect tópicos em centenas toothousands de registos. Tenha em atenção que esta API cobra uma transação por registo de texto submetido. Olá API é toowork concebida para humanos curto, escrito texto como revisões e comentários dos utilizadores.

- - -
## <a name="api-definition"></a>Definição da API
### <a name="headers"></a>Cabeçalhos
Certifique-se de que inclui cabeçalhos correto Olá do seu pedido, o que deve ser o seguinte:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Pode encontrar a chave da conta da sua conta em Olá [mercado de dados do Azure](https://datamarket.azure.com/account/keys). Tenha em atenção que o JSON de momento, apenas é aceite para formatos de entrada e de saída. XML não é suportado.

- - -
## <a name="single-response-apis"></a>APIs de resposta único
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Exemplo de pedido**

Na chamada de Olá abaixo, iremos está a pedir análise de dados de sentimento para a expressão de Olá "Olá mundo":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Esta ação irá devolver uma resposta da seguinte forma:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Exemplo de pedido**

Na chamada de Olá abaixo, iremos está a pedir expressões chave Olá encontrado no texto de Olá "Era um wonderful toostay de átrios no, com décor exclusivo e funcionários amigáveis":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Esta ação irá devolver uma resposta da seguinte forma:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Exemplo de pedido**

Na chamada GET Olá abaixo, iremos estão a pedir sentimento Olá para expressões de chave Olá no texto Olá *Olá mundo*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Esta ação irá devolver uma resposta da seguinte forma:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Parâmetros opcionais**

`NumberOfLanguagesToDetect`é um parâmetro opcional. Olá predefinição é 1.

- - -
## <a name="batch-apis"></a>APIs do batch
Olá serviço análise de texto permite toodo sentimento e extrações de expressão de chave no modo de batch. Tenha em atenção que cada um dos registos de Olá classificada contagens como uma transação. Por exemplo, se pedido sentimento para registos de 1000 numa única chamada, 1000 transações irão ser deducted.

Tenha em atenção que os IDs de Olá introduzidos no sistema de Olá são os IDs de Olá devolvidos pelo sistema Olá. serviço web de Olá não verifica se estes IDs são exclusivos. É Olá responsabilidade de exclusividade de tooverify Olá autor da chamada. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Exemplo de pedido**

No Olá POST chame abaixo, estamos a pedir para sentiments Olá das expressões Olá "Olá mundo", "Olá mundo de Foo" e "Olá My mundo" no corpo de Olá de pedido de Olá:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Corpo do pedido:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Resposta de Olá abaixo, a obter lista de Olá de pontuações associados com o seu texto de Ids de:

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Exemplo de pedido**

Neste exemplo, vamos pedir para Olá obter lista de sentiments para expressões de chave Olá no Olá textos os seguintes: 

* "Foi um wonderful toostay de átrios no, com décor exclusivo e funcionários amigáveis"
* "Foi uma conferência compilação incrível, com muito interessantes talks"
* "tráfego Olá foi terríveis, despendido a três horas vai toohello airport"

Este pedido é efetuado como um ponto final toohello de chamada POST:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Corpo do pedido:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Resposta de Olá abaixo, obter lista Olá das expressões de chaves associados com o seu texto de Ids de:

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

Na chamada POST Olá abaixo, iremos está a pedir a deteção de idioma para duas entradas de texto:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Corpo do pedido:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Esta ação devolve Olá resposta, a seguir onde inglês for detetado em Olá primeira entrada e francês na entrada segundo Olá:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>APIs de deteção de tópico
Esta é uma API recentemente publicada que devolve Olá principais tópicos detetado para obter uma lista de registos de texto foi submetido. É identificado um tópico com uma expressão chave, a qual pode ser constituída por uma ou mais palavras relacionadas. Tenha em atenção que esta API cobra uma transação por registo de texto submetido.

Esta API requer um mínimo de texto 100 regista toobe submetido, mas é concebida toodetect tópicos em centenas toothousands de registos.

### <a name="topics--submit-job"></a>Tópicos – submeter tarefa
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Exemplo de pedido**

Na chamada POST Olá abaixo, iremos está a pedir tópicos para um conjunto de 100 artigos, onde Olá primeiro e último entrada artigos são apresentados, e duas StopPhrases estão incluídos.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Corpo do pedido:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Resposta de Olá abaixo, obter Olá JobId para a tarefa submetido Olá:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Uma lista de palavra única ou várias expressões palavra que não devem ser devolvidos como tópicos. Pode ser utilizado toofilter saída tópicos muito genéricos. Por exemplo, um conjunto de dados sobre revisões átrios, "átrios" e "hostel" pode ser paragem sensible expressões.  

### <a name="topics--poll-for-job-results"></a>Resultados de consulta para a tarefa de tópicos –
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Exemplo de pedido**

Passe Olá que JobId devolvido de Olá 'Submeter tarefa' passo toofetch Olá resulta. Recomendamos que chamar este ponto final de cada minuto até que o estado = 'Concluída' na resposta Olá. Irá demorar cerca de 10 minutos para toocomplete uma tarefa, ou superior para as tarefas com muitos milhares de registos.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Enquanto estiver a processar, resposta Olá será o seguinte:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Olá API devolve o resultado no formato JSON no Olá seguinte formato:

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


Olá as propriedades de cada parte da resposta Olá são os seguintes:

**Propriedades de TopicInfo**

| Chave | Descrição |
|:--- |:--- |
| TopicId |Um identificador exclusivo para cada tópico. |
| Classificação |Contagem de registos atribuído tootopic. |
| KeyPhrase |Uma summarizing palavra ou expressão de tópico Olá. Pode ser 1 ou várias palavras. |

**Propriedades de TopicAssignment**

| Chave | Descrição |
|:--- |:--- |
| Id |Identificador de registo de Olá. Equivale ID toohello incluído na entrada de Olá. |
| TopicId |ID de tópico Olá que Olá registo foi atribuído. |
| Distância |Confiança de que o registo de Olá pertence toohello tópico. Toozero próximo distância indica maior confiança. |

