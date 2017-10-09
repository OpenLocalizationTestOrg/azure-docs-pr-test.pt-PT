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
# <a name="deprecated-difference-in-proportions-test"></a>(preterido) Diferença nas proporções teste

> [!NOTE]
> Olá Microsoft DataMarket vai ser reformado e esta API foi preterida. 
> 
> Para encontrar muitas APIs e experimentações de exemplo útil Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [partilha e detetar recursos na Olá galeria da Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).

São duas as proporções estatisticamente diferentes? Suponha que um utilizador pretende toocompare dois filmes toodetermine se um filme tem uma significativamente maior proporção de 'likes' quando comparado com toohello outro. Com um grande de exemplo, pode haver uma diferença significativa estatisticamente entre Olá as proporções 0.50 e 0.51. Com um pequeno de exemplo, poderá não existir suficiente toodetermine de dados se estes proporções são realmente diferentes. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Isto [serviço web](https://datamarket.azure.com/dataset/aml_labs/prop_test) efetua um teste de hipótese de diferença de Olá nos dois as proporções com base na entrada de utilizador do número de Olá de êxitos e o número total de Olá de avaliações de grupos de comparação de Olá 2. Um cenário possíveis, este serviço web pode ser chamado a partir de dentro de uma aplicação de comparação de filmes, informar o utilizador de Olá se um dos filmes Olá é realmente 'gostou' mais frequentemente Olá outro, com base em classificações de filmes.

> Este serviço web que pode ser utilizado por utilizadores – potencialmente através de uma aplicação móvel, através de um Web site, ou mesmo num computador local, por exemplo. Mas objetivo Olá do serviço web de Olá também tooserve como um exemplo de como o Azure Machine Learning podem ser serviços web de toocreate utilizado por cima do código do R. Com apenas alguns linhas de código do R e os cliques em de um botão no Azure Machine Learning Studio, uma experimentação pode ser criada com o código do R e publicada como um serviço web. serviço web de Olá, em seguida, pode ser publicada toohello Azure Marketplace e consumidas por utilizadores e dispositivos em Olá mundo com nenhuma configuração de infraestrutura pelo autor Olá do serviço web de Olá.
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço web
Este serviço aceita 4 argumentos e um hipótese de teste das proporções.

os argumentos de entrada de Olá são:

* Successes1 - número de eventos de êxito exemplo 1.
* Successes2 - número de eventos de êxito exemplo 2.
* Total1 - tamanho de exemplo 1.
* Total2 - tamanho de exemplo 2.

saída de Olá do serviço de Olá é o resultado de Olá da hipótese de Olá testar juntamente com Olá chi-square estatística, df, p-valor e a proporção em limites de 1/2 e o intervalo de confiança de exemplo.

> Este serviço alojado no Azure Marketplace, de Olá é um serviço OData; Estes podem ser chamados através de métodos POST ou GET. 
> 
> 

Existem várias formas de consumir o serviço de Olá de forma automática (uma aplicação de exemplo está [aqui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>A iniciar código c# para o consumo do serviço web:
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


## <a name="creation-of-web-service"></a>Criação do serviço web
> Este serviço web foi criado utilizando o Azure Machine Learning. Para uma avaliação gratuita, bem como vídeos introdutórias sobre a criação de experimentações e [publicação de serviços web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Segue-se uma captura de ecrã da experimentação Olá que criou o código de exemplo e do serviço da web Olá para cada um dos módulos de Olá na experimentação de Olá.
> 
> 

No Azure Machine Learning, uma nova experimentação em branco foi criada com dois [executar Script do R] [ execute-r-script] módulos. Esquema de dados de Olá está definida no módulo primeiro Olá, enquanto módulo segundo Olá utiliza o comando de prop.test Olá dentro de teste do R tooperform Olá hipótese para as 2 proporções. 

### <a name="experiment-flow"></a>Fluxo de experimentação:
![Fluxo de experimentação][2]

#### <a name="module-1"></a>Módulo 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Módulo de 2:
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


## <a name="limitations"></a>Limitações
Este é um exemplo muito simple para um teste de diferença nas 2 proporções. Como podem ser vistos a partir do código de exemplo de Olá acima, a não deteção de erro é implementado e serviço Olá parte do pressuposto de que todas as variáveis de Olá contínuas.

## <a name="faq"></a>FAQ
Para perguntas mais frequentes sobre o consumo do serviço web de Olá ou toohello publicação do Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

