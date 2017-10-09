---
title: "AAA(deprecated) classificador binário - Azure | Microsoft Docs"
description: "(preterido) Classificador de binário"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="0fa16-103">(preterido) Classificador de binário</span><span class="sxs-lookup"><span data-stu-id="0fa16-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="0fa16-104">Olá Microsoft DataMarket vai ser reformado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="0fa16-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0fa16-105">Para encontrar muitas APIs e experimentações de exemplo útil Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0fa16-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0fa16-106">Para obter mais informações sobre Olá galeria, consulte [partilha e detetar recursos na Olá galeria da Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0fa16-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0fa16-107">Suponha que tem um conjunto de dados e gostaria de toopredict uma variável dependentes binária com base nas variáveis independentes de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="0fa16-108">'Regressão logística da' é uma técnica de análises popular utilizada para essas predições.</span><span class="sxs-lookup"><span data-stu-id="0fa16-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0fa16-109">Eis Olá dependentes variável binário ou dichotomous e p é a probabilidade de Olá da presença característica Olá de interesse.</span><span class="sxs-lookup"><span data-stu-id="0fa16-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0fa16-110">Um cenário simples poderia ser onde um researcher está a tentar toopredict se um estudante potencial é provavelmente tooaccept um university de tooa de oferta admissão com base nas informações (GPA na escola, receitas de família, estado residente, sexo).</span><span class="sxs-lookup"><span data-stu-id="0fa16-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="0fa16-111">resultado previstas Olá é a probabilidade de Olá do estudante potenciais Olá aceitar Olá admissão oferta.</span><span class="sxs-lookup"><span data-stu-id="0fa16-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="0fa16-112">Isto [serviço web](https://datamarket.azure.com/dataset/aml_labs/log_regression) se adequa Olá dados de toohello do modelo de regressão logística da e saídas hello valor de probabilidade (s) para cada um das observações de Olá nos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="0fa16-113">Este serviço web que pode ser utilizado por utilizadores – potencialmente através de uma aplicação móvel, através de um Web site, ou mesmo num computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="0fa16-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0fa16-114">Mas objetivo Olá do serviço web de Olá também tooserve como um exemplo de como o Azure Machine Learning podem ser serviços web de toocreate utilizado por cima do código do R.</span><span class="sxs-lookup"><span data-stu-id="0fa16-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="0fa16-115">Com apenas alguns linhas de código do R e os cliques em de um botão no Azure Machine Learning Studio, uma experimentação pode ser criada com o código do R e publicada como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="0fa16-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0fa16-116">serviço web de Olá, em seguida, pode ser publicada toohello Azure Marketplace e consumidas por utilizadores e dispositivos em Olá mundo com nenhuma configuração de infraestrutura pelo autor Olá do serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0fa16-117">Consumo do serviço web</span><span class="sxs-lookup"><span data-stu-id="0fa16-117">Consumption of web service</span></span>
<span data-ttu-id="0fa16-118">Este Olá do web service fornecem prever valores da variável de dependentes Olá com base nas variáveis independentes de Olá para todas as observações de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="0fa16-119">serviço web de Olá espera dados de tooinput do utilizador final Olá como uma cadeia em que as linhas são separadas por vírgula (,) e colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="0fa16-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="0fa16-120">serviço web de Olá espera 1 linha de cada vez e espera Olá primeira coluna toobe Olá dependentes variável.</span><span class="sxs-lookup"><span data-stu-id="0fa16-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="0fa16-121">Um conjunto de dados de exemplo foi ter este aspeto:</span><span class="sxs-lookup"><span data-stu-id="0fa16-121">An example dataset could look like this:</span></span>

![Dados de exemplo][1]

<span data-ttu-id="0fa16-123">As observações sem uma variável de dependentes devem ser introduzidas como "ND" para y.</span><span class="sxs-lookup"><span data-stu-id="0fa16-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0fa16-124">Olá dados de entrada para Olá acima conjunto de dados deverá ser Olá seguinte cadeia: "1; 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="0fa16-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="0fa16-125">Olá de saída é hello valor previsto para cada uma das linhas de Olá com base nas variáveis independentes de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="0fa16-126">Este serviço alojado no Azure Marketplace, de Olá é um serviço OData; Estes podem ser chamados através de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="0fa16-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0fa16-127">Existem várias formas de consumir o serviço de Olá de forma automática (uma aplicação de exemplo está [aqui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0fa16-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0fa16-128">A iniciar código c# para o consumo do serviço web:</span><span class="sxs-lookup"><span data-stu-id="0fa16-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="0fa16-129">Criação do serviço web</span><span class="sxs-lookup"><span data-stu-id="0fa16-129">Creation of web service</span></span>
> <span data-ttu-id="0fa16-130">Este serviço web foi criado utilizando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0fa16-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0fa16-131">Para uma avaliação gratuita, bem como vídeos introdutórias sobre a criação de experimentações e [publicação de serviços web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0fa16-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0fa16-132">Segue-se uma captura de ecrã da experimentação Olá que criou o código de exemplo e do serviço da web Olá para cada um dos módulos de Olá na experimentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="0fa16-133">No Azure Machine Learning, foi criada uma nova experimentação em branco e dois [executar Script do R] [ execute-r-script] módulos solicitados na área de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="0fa16-134">Este serviço web executa uma experimentação do Azure Machine Learning com um script do R subjacente.</span><span class="sxs-lookup"><span data-stu-id="0fa16-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0fa16-135">Existem 2 partes toothis experimentação: definição de esquema e modelo de formação + classificação.</span><span class="sxs-lookup"><span data-stu-id="0fa16-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0fa16-136">módulo primeiro Olá define a estrutura de Olá esperado de Olá entrada conjunto de dados, onde variável primeiro Olá é Olá dependentes variável e variáveis restantes Olá são independentes.</span><span class="sxs-lookup"><span data-stu-id="0fa16-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="0fa16-137">módulo segundo Olá encaixa um modelo de regressão logística da genérico para dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="0fa16-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Fluxo de experimentação][2]

#### <a name="module-1"></a><span data-ttu-id="0fa16-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="0fa16-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0fa16-140">Módulo de 2:</span><span class="sxs-lookup"><span data-stu-id="0fa16-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="0fa16-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="0fa16-141">Limitations</span></span>
<span data-ttu-id="0fa16-142">Este é um exemplo muito simple de um serviço web de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="0fa16-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="0fa16-143">Como podem ser vistos a partir do código de exemplo de Olá acima, obtendo nenhum erro se encontra implementado e serviço Olá pressupõe que tudo está uma variável binário contínua (nenhum categórico funcionalidades permitidas), como Olá serviço apenas entradas valores numéricos momento Olá da criação de Olá deste serviço Web.</span><span class="sxs-lookup"><span data-stu-id="0fa16-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="0fa16-144">Além disso, serviço Olá atualmente processa o tamanho dos dados limitado, devido toohello natureza de pedido/resposta do serviço web de Olá facto de chamada e Olá Olá modelo está a ser caber sempre que o serviço web de Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="0fa16-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0fa16-145">FAQ</span><span class="sxs-lookup"><span data-stu-id="0fa16-145">FAQ</span></span>
<span data-ttu-id="0fa16-146">Para perguntas mais frequentes sobre o consumo do serviço web de Olá ou toohello publicação do Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0fa16-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

