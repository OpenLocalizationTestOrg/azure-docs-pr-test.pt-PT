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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="bec6f-103">APIs de Machine Learning: Análise de Texto para Sentimentos, Extração de Expressões-Chave, Deteção de Idioma e Deteção de Tópicos</span><span class="sxs-lookup"><span data-stu-id="bec6f-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="bec6f-104">Este guia destina-se a versão 1 do Olá API.</span><span class="sxs-lookup"><span data-stu-id="bec6f-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="bec6f-105">Para a versão 2, [ **Consulte toothis documento**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="bec6f-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="bec6f-106">Versão 2 está agora versão preferencial de Olá desta API.</span><span class="sxs-lookup"><span data-stu-id="bec6f-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="bec6f-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="bec6f-107">Overview</span></span>
<span data-ttu-id="bec6f-108">Olá API de análise de texto é um conjunto de análise de texto [serviços web](https://datamarket.azure.com/dataset/amla/text-analytics) criadas com o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bec6f-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="bec6f-109">Olá API pode ser utilizado tooanalyze texto não estruturado para tarefas como a análise de dados de sentimento, extração de expressão de chave, deteção de idioma e deteção de tópico.</span><span class="sxs-lookup"><span data-stu-id="bec6f-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="bec6f-110">Não são de dados de formação necessário toouse esta API: apenas colocar os dados de texto.</span><span class="sxs-lookup"><span data-stu-id="bec6f-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="bec6f-111">Esta API utiliza avançada linguagem natural processamento técnicas toodeliver melhor no predições de classe.</span><span class="sxs-lookup"><span data-stu-id="bec6f-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="bec6f-112">Pode ver análise de texto em ação na nossa [site demonstração](https://text-analytics-demo.azurewebsites.net/), onde também encontrará [amostras](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sobre como tooimplement análise de texto em c# e Python.</span><span class="sxs-lookup"><span data-stu-id="bec6f-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="bec6f-113">Análise de sentimentos</span><span class="sxs-lookup"><span data-stu-id="bec6f-113">Sentiment analysis</span></span>
<span data-ttu-id="bec6f-114">Olá API devolve uma pontuação numérico entre 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="bec6f-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="bec6f-115">Too1 fechar pontuações indicar sentimento positivo, enquanto too0 fechar pontuações indicar sentimento negativo.</span><span class="sxs-lookup"><span data-stu-id="bec6f-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="bec6f-116">A pontuação do sentimento é gerada através de técnicas de classificação.</span><span class="sxs-lookup"><span data-stu-id="bec6f-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="bec6f-117">Olá funcionalidades entrada toohello classificador incluem n-grams, geradas a partir de etiquetas de parte de voz e o word embeddings de funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="bec6f-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="bec6f-118">Atualmente, o inglês é Olá idioma suportado apenas.</span><span class="sxs-lookup"><span data-stu-id="bec6f-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="bec6f-119">Extração de expressões chave</span><span class="sxs-lookup"><span data-stu-id="bec6f-119">Key phrase extraction</span></span>
<span data-ttu-id="bec6f-120">Olá API devolve uma lista de cadeias que indica Olá chave talking pontos de texto de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="bec6f-121">Utilizamos técnicas do toolkit de Processamento de Linguagens Naturais do Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="bec6f-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="bec6f-122">Atualmente, o inglês é Olá idioma suportado apenas.</span><span class="sxs-lookup"><span data-stu-id="bec6f-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="bec6f-123">Deteção de idioma</span><span class="sxs-lookup"><span data-stu-id="bec6f-123">Language detection</span></span>
<span data-ttu-id="bec6f-124">Olá API devolve Olá detetou linguagem e uma pontuação numérico entre 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="bec6f-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="bec6f-125">Too1 fechar pontuações indicar certainty 100% se idioma Olá identificado é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="bec6f-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="bec6f-126">É suportado um total de 120 idiomas.</span><span class="sxs-lookup"><span data-stu-id="bec6f-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="bec6f-127">Deteção de tópicos</span><span class="sxs-lookup"><span data-stu-id="bec6f-127">Topic detection</span></span>
<span data-ttu-id="bec6f-128">Esta é uma API recentemente publicada que devolve Olá principais tópicos detetado para obter uma lista de registos de texto foi submetido.</span><span class="sxs-lookup"><span data-stu-id="bec6f-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="bec6f-129">É identificado um tópico com uma expressão chave, a qual pode ser constituída por uma ou mais palavras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="bec6f-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="bec6f-130">Esta API requer um mínimo de texto 100 regista toobe submetido, mas é concebida toodetect tópicos em centenas toothousands de registos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="bec6f-131">Tenha em atenção que esta API cobra uma transação por registo de texto submetido.</span><span class="sxs-lookup"><span data-stu-id="bec6f-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="bec6f-132">Olá API é toowork concebida para humanos curto, escrito texto como revisões e comentários dos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="bec6f-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="bec6f-133">Definição da API</span><span class="sxs-lookup"><span data-stu-id="bec6f-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="bec6f-134">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="bec6f-134">Headers</span></span>
<span data-ttu-id="bec6f-135">Certifique-se de que inclui cabeçalhos correto Olá do seu pedido, o que deve ser o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bec6f-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="bec6f-136">Pode encontrar a chave da conta da sua conta em Olá [mercado de dados do Azure](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="bec6f-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="bec6f-137">Tenha em atenção que o JSON de momento, apenas é aceite para formatos de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="bec6f-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="bec6f-138">XML não é suportado.</span><span class="sxs-lookup"><span data-stu-id="bec6f-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="bec6f-139">APIs de resposta único</span><span class="sxs-lookup"><span data-stu-id="bec6f-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="bec6f-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="bec6f-140">GetSentiment</span></span>
<span data-ttu-id="bec6f-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="bec6f-142">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-142">**Example request**</span></span>

<span data-ttu-id="bec6f-143">Na chamada de Olá abaixo, iremos está a pedir análise de dados de sentimento para a expressão de Olá "Olá mundo":</span><span class="sxs-lookup"><span data-stu-id="bec6f-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="bec6f-144">Esta ação irá devolver uma resposta da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="bec6f-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="bec6f-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="bec6f-145">GetKeyPhrases</span></span>
<span data-ttu-id="bec6f-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="bec6f-147">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-147">**Example request**</span></span>

<span data-ttu-id="bec6f-148">Na chamada de Olá abaixo, iremos está a pedir expressões chave Olá encontrado no texto de Olá "Era um wonderful toostay de átrios no, com décor exclusivo e funcionários amigáveis":</span><span class="sxs-lookup"><span data-stu-id="bec6f-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="bec6f-149">Esta ação irá devolver uma resposta da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="bec6f-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="bec6f-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="bec6f-150">GetLanguage</span></span>
<span data-ttu-id="bec6f-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="bec6f-152">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-152">**Example request**</span></span>

<span data-ttu-id="bec6f-153">Na chamada GET Olá abaixo, iremos estão a pedir sentimento Olá para expressões de chave Olá no texto Olá *Olá mundo*</span><span class="sxs-lookup"><span data-stu-id="bec6f-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="bec6f-154">Esta ação irá devolver uma resposta da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="bec6f-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="bec6f-155">**Parâmetros opcionais**</span><span class="sxs-lookup"><span data-stu-id="bec6f-155">**Optional parameters**</span></span>

<span data-ttu-id="bec6f-156">`NumberOfLanguagesToDetect`é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="bec6f-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="bec6f-157">Olá predefinição é 1.</span><span class="sxs-lookup"><span data-stu-id="bec6f-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="bec6f-158">APIs do batch</span><span class="sxs-lookup"><span data-stu-id="bec6f-158">Batch APIs</span></span>
<span data-ttu-id="bec6f-159">Olá serviço análise de texto permite toodo sentimento e extrações de expressão de chave no modo de batch.</span><span class="sxs-lookup"><span data-stu-id="bec6f-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="bec6f-160">Tenha em atenção que cada um dos registos de Olá classificada contagens como uma transação.</span><span class="sxs-lookup"><span data-stu-id="bec6f-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="bec6f-161">Por exemplo, se pedido sentimento para registos de 1000 numa única chamada, 1000 transações irão ser deducted.</span><span class="sxs-lookup"><span data-stu-id="bec6f-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="bec6f-162">Tenha em atenção que os IDs de Olá introduzidos no sistema de Olá são os IDs de Olá devolvidos pelo sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="bec6f-163">serviço web de Olá não verifica se estes IDs são exclusivos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="bec6f-164">É Olá responsabilidade de exclusividade de tooverify Olá autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="bec6f-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="bec6f-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="bec6f-165">GetSentimentBatch</span></span>
<span data-ttu-id="bec6f-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="bec6f-167">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-167">**Example request**</span></span>

<span data-ttu-id="bec6f-168">No Olá POST chame abaixo, estamos a pedir para sentiments Olá das expressões Olá "Olá mundo", "Olá mundo de Foo" e "Olá My mundo" no corpo de Olá de pedido de Olá:</span><span class="sxs-lookup"><span data-stu-id="bec6f-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="bec6f-169">Corpo do pedido:</span><span class="sxs-lookup"><span data-stu-id="bec6f-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="bec6f-170">Resposta de Olá abaixo, a obter lista de Olá de pontuações associados com o seu texto de Ids de:</span><span class="sxs-lookup"><span data-stu-id="bec6f-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="bec6f-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="bec6f-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="bec6f-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="bec6f-173">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-173">**Example request**</span></span>

<span data-ttu-id="bec6f-174">Neste exemplo, vamos pedir para Olá obter lista de sentiments para expressões de chave Olá no Olá textos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bec6f-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="bec6f-175">"Foi um wonderful toostay de átrios no, com décor exclusivo e funcionários amigáveis"</span><span class="sxs-lookup"><span data-stu-id="bec6f-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="bec6f-176">"Foi uma conferência compilação incrível, com muito interessantes talks"</span><span class="sxs-lookup"><span data-stu-id="bec6f-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="bec6f-177">"tráfego Olá foi terríveis, despendido a três horas vai toohello airport"</span><span class="sxs-lookup"><span data-stu-id="bec6f-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="bec6f-178">Este pedido é efetuado como um ponto final toohello de chamada POST:</span><span class="sxs-lookup"><span data-stu-id="bec6f-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="bec6f-179">Corpo do pedido:</span><span class="sxs-lookup"><span data-stu-id="bec6f-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="bec6f-180">Resposta de Olá abaixo, obter lista Olá das expressões de chaves associados com o seu texto de Ids de:</span><span class="sxs-lookup"><span data-stu-id="bec6f-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="bec6f-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="bec6f-181">GetLanguageBatch</span></span>

<span data-ttu-id="bec6f-182">Na chamada POST Olá abaixo, iremos está a pedir a deteção de idioma para duas entradas de texto:</span><span class="sxs-lookup"><span data-stu-id="bec6f-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="bec6f-183">Corpo do pedido:</span><span class="sxs-lookup"><span data-stu-id="bec6f-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="bec6f-184">Esta ação devolve Olá resposta, a seguir onde inglês for detetado em Olá primeira entrada e francês na entrada segundo Olá:</span><span class="sxs-lookup"><span data-stu-id="bec6f-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="bec6f-185">APIs de deteção de tópico</span><span class="sxs-lookup"><span data-stu-id="bec6f-185">Topic Detection APIs</span></span>
<span data-ttu-id="bec6f-186">Esta é uma API recentemente publicada que devolve Olá principais tópicos detetado para obter uma lista de registos de texto foi submetido.</span><span class="sxs-lookup"><span data-stu-id="bec6f-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="bec6f-187">É identificado um tópico com uma expressão chave, a qual pode ser constituída por uma ou mais palavras relacionadas.</span><span class="sxs-lookup"><span data-stu-id="bec6f-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="bec6f-188">Tenha em atenção que esta API cobra uma transação por registo de texto submetido.</span><span class="sxs-lookup"><span data-stu-id="bec6f-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="bec6f-189">Esta API requer um mínimo de texto 100 regista toobe submetido, mas é concebida toodetect tópicos em centenas toothousands de registos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="bec6f-190">Tópicos – submeter tarefa</span><span class="sxs-lookup"><span data-stu-id="bec6f-190">Topics – Submit job</span></span>
<span data-ttu-id="bec6f-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="bec6f-192">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-192">**Example request**</span></span>

<span data-ttu-id="bec6f-193">Na chamada POST Olá abaixo, iremos está a pedir tópicos para um conjunto de 100 artigos, onde Olá primeiro e último entrada artigos são apresentados, e duas StopPhrases estão incluídos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="bec6f-194">Corpo do pedido:</span><span class="sxs-lookup"><span data-stu-id="bec6f-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="bec6f-195">Resposta de Olá abaixo, obter Olá JobId para a tarefa submetido Olá:</span><span class="sxs-lookup"><span data-stu-id="bec6f-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="bec6f-196">Uma lista de palavra única ou várias expressões palavra que não devem ser devolvidos como tópicos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="bec6f-197">Pode ser utilizado toofilter saída tópicos muito genéricos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="bec6f-198">Por exemplo, um conjunto de dados sobre revisões átrios, "átrios" e "hostel" pode ser paragem sensible expressões.</span><span class="sxs-lookup"><span data-stu-id="bec6f-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="bec6f-199">Resultados de consulta para a tarefa de tópicos –</span><span class="sxs-lookup"><span data-stu-id="bec6f-199">Topics – Poll for job results</span></span>
<span data-ttu-id="bec6f-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="bec6f-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="bec6f-201">**Exemplo de pedido**</span><span class="sxs-lookup"><span data-stu-id="bec6f-201">**Example request**</span></span>

<span data-ttu-id="bec6f-202">Passe Olá que JobId devolvido de Olá 'Submeter tarefa' passo toofetch Olá resulta.</span><span class="sxs-lookup"><span data-stu-id="bec6f-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="bec6f-203">Recomendamos que chamar este ponto final de cada minuto até que o estado = 'Concluída' na resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="bec6f-204">Irá demorar cerca de 10 minutos para toocomplete uma tarefa, ou superior para as tarefas com muitos milhares de registos.</span><span class="sxs-lookup"><span data-stu-id="bec6f-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="bec6f-205">Enquanto estiver a processar, resposta Olá será o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bec6f-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="bec6f-206">Olá API devolve o resultado no formato JSON no Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="bec6f-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="bec6f-207">Olá as propriedades de cada parte da resposta Olá são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bec6f-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="bec6f-208">**Propriedades de TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="bec6f-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="bec6f-209">Chave</span><span class="sxs-lookup"><span data-stu-id="bec6f-209">Key</span></span> | <span data-ttu-id="bec6f-210">Descrição</span><span class="sxs-lookup"><span data-stu-id="bec6f-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bec6f-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="bec6f-211">TopicId</span></span> |<span data-ttu-id="bec6f-212">Um identificador exclusivo para cada tópico.</span><span class="sxs-lookup"><span data-stu-id="bec6f-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="bec6f-213">Classificação</span><span class="sxs-lookup"><span data-stu-id="bec6f-213">Score</span></span> |<span data-ttu-id="bec6f-214">Contagem de registos atribuído tootopic.</span><span class="sxs-lookup"><span data-stu-id="bec6f-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="bec6f-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="bec6f-215">KeyPhrase</span></span> |<span data-ttu-id="bec6f-216">Uma summarizing palavra ou expressão de tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="bec6f-217">Pode ser 1 ou várias palavras.</span><span class="sxs-lookup"><span data-stu-id="bec6f-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="bec6f-218">**Propriedades de TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="bec6f-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="bec6f-219">Chave</span><span class="sxs-lookup"><span data-stu-id="bec6f-219">Key</span></span> | <span data-ttu-id="bec6f-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="bec6f-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bec6f-221">Id</span><span class="sxs-lookup"><span data-stu-id="bec6f-221">Id</span></span> |<span data-ttu-id="bec6f-222">Identificador de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-222">Identifier for hello record.</span></span> <span data-ttu-id="bec6f-223">Equivale ID toohello incluído na entrada de Olá.</span><span class="sxs-lookup"><span data-stu-id="bec6f-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="bec6f-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="bec6f-224">TopicId</span></span> |<span data-ttu-id="bec6f-225">ID de tópico Olá que Olá registo foi atribuído.</span><span class="sxs-lookup"><span data-stu-id="bec6f-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="bec6f-226">Distância</span><span class="sxs-lookup"><span data-stu-id="bec6f-226">Distance</span></span> |<span data-ttu-id="bec6f-227">Confiança de que o registo de Olá pertence toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="bec6f-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="bec6f-228">Toozero próximo distância indica maior confiança.</span><span class="sxs-lookup"><span data-stu-id="bec6f-228">Distance closer toozero indicates higher confidence.</span></span> |

