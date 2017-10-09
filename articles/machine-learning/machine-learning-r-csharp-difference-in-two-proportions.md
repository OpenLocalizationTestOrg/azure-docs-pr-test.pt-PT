---
title: "AAA(deprecated) diferença no teste as proporções - Azure | Microsoft Docs"
description: "(preterido) Diferença nas proporções teste"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="d73ec-103">(preterido) Diferença nas proporções teste</span><span class="sxs-lookup"><span data-stu-id="d73ec-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="d73ec-104">Olá Microsoft DataMarket vai ser reformado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="d73ec-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d73ec-105">Para encontrar muitas APIs e experimentações de exemplo útil Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d73ec-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d73ec-106">Para obter mais informações sobre Olá galeria, consulte [partilha e detetar recursos na Olá galeria da Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d73ec-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d73ec-107">São duas as proporções estatisticamente diferentes?</span><span class="sxs-lookup"><span data-stu-id="d73ec-107">Are two proportions statistically different?</span></span> <span data-ttu-id="d73ec-108">Suponha que um utilizador pretende toocompare dois filmes toodetermine se um filme tem uma significativamente maior proporção de 'likes' quando comparado com toohello outro.</span><span class="sxs-lookup"><span data-stu-id="d73ec-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="d73ec-109">Com um grande de exemplo, pode haver uma diferença significativa estatisticamente entre Olá as proporções 0.50 e 0.51.</span><span class="sxs-lookup"><span data-stu-id="d73ec-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="d73ec-110">Com um pequeno de exemplo, poderá não existir suficiente toodetermine de dados se estes proporções são realmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="d73ec-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d73ec-111">Isto [serviço web](https://datamarket.azure.com/dataset/aml_labs/prop_test) efetua um teste de hipótese de diferença de Olá nos dois as proporções com base na entrada de utilizador do número de Olá de êxitos e o número total de Olá de avaliações de grupos de comparação de Olá 2.</span><span class="sxs-lookup"><span data-stu-id="d73ec-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="d73ec-112">Um cenário possíveis, este serviço web pode ser chamado a partir de dentro de uma aplicação de comparação de filmes, informar o utilizador de Olá se um dos filmes Olá é realmente 'gostou' mais frequentemente Olá outro, com base em classificações de filmes.</span><span class="sxs-lookup"><span data-stu-id="d73ec-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="d73ec-113">Este serviço web que pode ser utilizado por utilizadores – potencialmente através de uma aplicação móvel, através de um Web site, ou mesmo num computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="d73ec-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d73ec-114">Mas objetivo Olá do serviço web de Olá também tooserve como um exemplo de como o Azure Machine Learning podem ser serviços web de toocreate utilizado por cima do código do R.</span><span class="sxs-lookup"><span data-stu-id="d73ec-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="d73ec-115">Com apenas alguns linhas de código do R e os cliques em de um botão no Azure Machine Learning Studio, uma experimentação pode ser criada com o código do R e publicada como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="d73ec-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d73ec-116">serviço web de Olá, em seguida, pode ser publicada toohello Azure Marketplace e consumidas por utilizadores e dispositivos em Olá mundo com nenhuma configuração de infraestrutura pelo autor Olá do serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="d73ec-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d73ec-117">Consumo do serviço web</span><span class="sxs-lookup"><span data-stu-id="d73ec-117">Consumption of web service</span></span>
<span data-ttu-id="d73ec-118">Este serviço aceita 4 argumentos e um hipótese de teste das proporções.</span><span class="sxs-lookup"><span data-stu-id="d73ec-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="d73ec-119">os argumentos de entrada de Olá são:</span><span class="sxs-lookup"><span data-stu-id="d73ec-119">hello input arguments are:</span></span>

* <span data-ttu-id="d73ec-120">Successes1 - número de eventos de êxito exemplo 1.</span><span class="sxs-lookup"><span data-stu-id="d73ec-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="d73ec-121">Successes2 - número de eventos de êxito exemplo 2.</span><span class="sxs-lookup"><span data-stu-id="d73ec-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="d73ec-122">Total1 - tamanho de exemplo 1.</span><span class="sxs-lookup"><span data-stu-id="d73ec-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="d73ec-123">Total2 - tamanho de exemplo 2.</span><span class="sxs-lookup"><span data-stu-id="d73ec-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="d73ec-124">saída de Olá do serviço de Olá é o resultado de Olá da hipótese de Olá testar juntamente com Olá chi-square estatística, df, p-valor e a proporção em limites de 1/2 e o intervalo de confiança de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d73ec-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="d73ec-125">Este serviço alojado no Azure Marketplace, de Olá é um serviço OData; Estes podem ser chamados através de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="d73ec-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d73ec-126">Existem várias formas de consumir o serviço de Olá de forma automática (uma aplicação de exemplo está [aqui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d73ec-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d73ec-127">A iniciar código c# para o consumo do serviço web:</span><span class="sxs-lookup"><span data-stu-id="d73ec-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="d73ec-128">Criação do serviço web</span><span class="sxs-lookup"><span data-stu-id="d73ec-128">Creation of web service</span></span>
> <span data-ttu-id="d73ec-129">Este serviço web foi criado utilizando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d73ec-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d73ec-130">Para uma avaliação gratuita, bem como vídeos introdutórias sobre a criação de experimentações e [publicação de serviços web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d73ec-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d73ec-131">Segue-se uma captura de ecrã da experimentação Olá que criou o código de exemplo e do serviço da web Olá para cada um dos módulos de Olá na experimentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d73ec-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="d73ec-132">No Azure Machine Learning, uma nova experimentação em branco foi criada com dois [executar Script do R] [ execute-r-script] módulos.</span><span class="sxs-lookup"><span data-stu-id="d73ec-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="d73ec-133">Esquema de dados de Olá está definida no módulo primeiro Olá, enquanto módulo segundo Olá utiliza o comando de prop.test Olá dentro de teste do R tooperform Olá hipótese para as 2 proporções.</span><span class="sxs-lookup"><span data-stu-id="d73ec-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="d73ec-134">Fluxo de experimentação:</span><span class="sxs-lookup"><span data-stu-id="d73ec-134">Experiment flow:</span></span>
![Fluxo de experimentação][2]

#### <a name="module-1"></a><span data-ttu-id="d73ec-136">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="d73ec-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="d73ec-137">Módulo de 2:</span><span class="sxs-lookup"><span data-stu-id="d73ec-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="d73ec-138">Limitações</span><span class="sxs-lookup"><span data-stu-id="d73ec-138">Limitations</span></span>
<span data-ttu-id="d73ec-139">Este é um exemplo muito simple para um teste de diferença nas 2 proporções.</span><span class="sxs-lookup"><span data-stu-id="d73ec-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="d73ec-140">Como podem ser vistos a partir do código de exemplo de Olá acima, a não deteção de erro é implementado e serviço Olá parte do pressuposto de que todas as variáveis de Olá contínuas.</span><span class="sxs-lookup"><span data-stu-id="d73ec-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="d73ec-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="d73ec-141">FAQ</span></span>
<span data-ttu-id="d73ec-142">Para perguntas mais frequentes sobre o consumo do serviço web de Olá ou toohello publicação do Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d73ec-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

