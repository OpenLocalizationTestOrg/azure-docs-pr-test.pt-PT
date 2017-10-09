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
# <a name="deprecated-binary-classifier"></a>(preterido) Classificador de binário

> [!NOTE]
> Olá Microsoft DataMarket vai ser reformado e esta API foi preterida. 
> 
> Para encontrar muitas APIs e experimentações de exemplo útil Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [partilha e detetar recursos na Olá galeria da Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).

Suponha que tem um conjunto de dados e gostaria de toopredict uma variável dependentes binária com base nas variáveis independentes de Olá. 'Regressão logística da' é uma técnica de análises popular utilizada para essas predições. Eis Olá dependentes variável binário ou dichotomous e p é a probabilidade de Olá da presença característica Olá de interesse. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Um cenário simples poderia ser onde um researcher está a tentar toopredict se um estudante potencial é provavelmente tooaccept um university de tooa de oferta admissão com base nas informações (GPA na escola, receitas de família, estado residente, sexo). resultado previstas Olá é a probabilidade de Olá do estudante potenciais Olá aceitar Olá admissão oferta. Isto [serviço web](https://datamarket.azure.com/dataset/aml_labs/log_regression) se adequa Olá dados de toohello do modelo de regressão logística da e saídas hello valor de probabilidade (s) para cada um das observações de Olá nos dados de Olá.  

> Este serviço web que pode ser utilizado por utilizadores – potencialmente através de uma aplicação móvel, através de um Web site, ou mesmo num computador local, por exemplo. Mas objetivo Olá do serviço web de Olá também tooserve como um exemplo de como o Azure Machine Learning podem ser serviços web de toocreate utilizado por cima do código do R. Com apenas alguns linhas de código do R e os cliques em de um botão no Azure Machine Learning Studio, uma experimentação pode ser criada com o código do R e publicada como um serviço web. serviço web de Olá, em seguida, pode ser publicada toohello Azure Marketplace e consumidas por utilizadores e dispositivos em Olá mundo com nenhuma configuração de infraestrutura pelo autor Olá do serviço web de Olá.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço web
Este Olá do web service fornecem prever valores da variável de dependentes Olá com base nas variáveis independentes de Olá para todas as observações de Olá. serviço web de Olá espera dados de tooinput do utilizador final Olá como uma cadeia em que as linhas são separadas por vírgula (,) e colunas são separadas por ponto e vírgula (;). serviço web de Olá espera 1 linha de cada vez e espera Olá primeira coluna toobe Olá dependentes variável. Um conjunto de dados de exemplo foi ter este aspeto:

![Dados de exemplo][1]

As observações sem uma variável de dependentes devem ser introduzidas como "ND" para y. Olá dados de entrada para Olá acima conjunto de dados deverá ser Olá seguinte cadeia: "1; 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4". Olá de saída é hello valor previsto para cada uma das linhas de Olá com base nas variáveis independentes de Olá. 

> Este serviço alojado no Azure Marketplace, de Olá é um serviço OData; Estes podem ser chamados através de métodos POST ou GET. 
> 
> 

Existem várias formas de consumir o serviço de Olá de forma automática (uma aplicação de exemplo está [aqui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>A iniciar código c# para o consumo do serviço web:
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


## <a name="creation-of-web-service"></a>Criação do serviço web
> Este serviço web foi criado utilizando o Azure Machine Learning. Para uma avaliação gratuita, bem como vídeos introdutórias sobre a criação de experimentações e [publicação de serviços web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Segue-se uma captura de ecrã da experimentação Olá que criou o código de exemplo e do serviço da web Olá para cada um dos módulos de Olá na experimentação de Olá.
> 
> 

No Azure Machine Learning, foi criada uma nova experimentação em branco e dois [executar Script do R] [ execute-r-script] módulos solicitados na área de trabalho Olá. Este serviço web executa uma experimentação do Azure Machine Learning com um script do R subjacente. Existem 2 partes toothis experimentação: definição de esquema e modelo de formação + classificação. módulo primeiro Olá define a estrutura de Olá esperado de Olá entrada conjunto de dados, onde variável primeiro Olá é Olá dependentes variável e variáveis restantes Olá são independentes. módulo segundo Olá encaixa um modelo de regressão logística da genérico para dados de entrada Olá.    

![Fluxo de experimentação][2]

#### <a name="module-1"></a>Módulo 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Módulo de 2:
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


## <a name="limitations"></a>Limitações
Este é um exemplo muito simple de um serviço web de classificação binária. Como podem ser vistos a partir do código de exemplo de Olá acima, obtendo nenhum erro se encontra implementado e serviço Olá pressupõe que tudo está uma variável binário contínua (nenhum categórico funcionalidades permitidas), como Olá serviço apenas entradas valores numéricos momento Olá da criação de Olá deste serviço Web. Além disso, serviço Olá atualmente processa o tamanho dos dados limitado, devido toohello natureza de pedido/resposta do serviço web de Olá facto de chamada e Olá Olá modelo está a ser caber sempre que o serviço web de Olá é chamado. 

## <a name="faq"></a>FAQ
Para perguntas mais frequentes sobre o consumo do serviço web de Olá ou toohello publicação do Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

