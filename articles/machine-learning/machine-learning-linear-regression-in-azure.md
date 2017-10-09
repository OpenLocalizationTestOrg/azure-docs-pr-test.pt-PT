---
title: "aaaUsing regressão Linear no Machine Learning | Microsoft Docs"
description: "Uma comparação dos modelos de regressão linear no Excel e no Azure Machine Learning Studio"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Utilizar a regressão linear no Azure Machine Learning
> *Kate Baroni* e *Bernardo Boatman* é enterprise os arquitetos de soluções dados Insights Centro de Excellence da Microsoft. Neste artigo, descrevem sua experiência de migrar uma regressão analysis suite tooa baseado na nuvem solução existente utilizando o Azure Machine Learning. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Objetivo
Nosso projeto começar a utilizar dois objetivos em mente: 

1. Utilize a Análise Preditiva tooimprove Olá exatidão projeções de receitas mensal nossa organização 
2. Utilizar o Azure Machine Learning tooconfirm, otimizar, aumentar a velocidade e a escala da nossa resultados. 

Como muitas empresas, nossa organização passa através de uma processo de previsão de receitas mensal. A nossa equipa pequena dos analistas de negócios foi lhes é incumbida através do Azure Machine Learning toosupport Olá processo e melhorar a exatidão da previsão. equipa de Olá despendido vários meses, a recolha de dados de várias origens e em execução atributos de dados de Olá através de análises que identifica os atributos de chave tooservices relevantes vendas de previsão. passo seguinte Olá foi modelos de regressão análises de fazer o protótipo toobegin nos dados de Olá no Excel. Dentro de algumas semanas, iremos tinha um modelo de regressão do Excel que foi outperforming campo atual Olá e financeiro processos de previsão. Isto ficou resultados de predição de linha de base de Olá. 

Em seguida, pegámos Olá seguinte passo toomoving nosso Análise Preditiva através de tooAzure Machine Learning toofind enviados como pode melhorar o Machine Learning no desempenho preditivo.

## <a name="achieving-predictive-performance-parity"></a>Alcançar paridade de desempenho preditiva
A nossa prioridade primeiro foi tooachieve paridade entre os modelos de regressão de Machine Learning e o Excel. Dada Olá mesmos dados e mesmo Dividir para formação e testar dados Olá, queremos paridade de desempenho preditiva tooachieve entre o Excel e Machine Learning. Inicialmente falha. modelo do Excel Olá outperformed modelo do Machine Learning Olá. Falha de Olá era devido a falta de tooa de compreensão da ferramenta base Olá no Machine Learning. Depois de uma sincronização com a equipa de produto do Machine Learning Olá, iremos este adquiriu uma melhor compreensão sobre Olá base definição necessária para a nossa conjuntos de dados e conseguido paridade entre dois modelos de Olá. 

### <a name="create-regression-model-in-excel"></a>Criar modelo de regressão no Excel
A nossa regressão Excel utilizado modelo de regressão linear padrão Olá encontrado no Olá ToolPak de análise do Excel. 

Iremos calculado *% absoluto média erro* e utilizado-lo como medida de desempenho de Olá para o modelo de Olá. Demorou tooarrive de 3 meses, um modelo de trabalhar com o Excel. É colocada muito learning Olá para Olá experimentação do Machine Learning Studio que, fundamentalmente, foi benéfico nos requisitos de compreender.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Criar comparável experimentação no Azure Machine Learning
Iremos seguido estes passos toocreate nosso experimentação no Machine Learning Studio: 

1. Conjunto de dados de Olá carregado como um tooMachine de ficheiro csv (ficheiro muito pequeno) do Learning Studio
2. Criar uma nova experimentação e utilizado Olá [selecionar colunas no conjunto de dados] [ select-columns] tooselect módulo Olá mesmo dados funcionalidades utilizadas no Excel 
3. Olá utilizado [dividir dados] [ split] módulo (com *expressão relativo* modo) dados de Olá toodivide para Olá conjuntos de dados de formação mesmo como tinha sido feito no Excel 
4. Experimented com Olá [regressão Linear] [ linear-regression] módulo (apenas opções predefinidas), documentados e, em comparação com o modelo de regressão do Olá resultados tooour Excel

### <a name="review-initial-results"></a>Reveja os resultados iniciais
Em primeiro lugar, o modelo do Excel Olá outperformed claramente modelo de Machine Learning Studio Olá: 

|  | Excel | Studio |
| --- |:---:|:---:|
| Desempenho | | |
| <ul style="list-style-type: none;"><li>Tendo em conta os parênteses de R</li></ul> |0.96 |N/D |
| <ul style="list-style-type: none;"><li>Coeficiente de <br />Determinação</li></ul> |N/D |0.78<br />(precisão baixa) |
| Tem de estar verdadeiramente erros absolutos |$9. 5M |$ 19.4 M |
| Tem de estar verdadeiramente erros absolutos (%) |6.03% |12.2% |

Quando executamos nosso processo e os resultados por programadores Olá e cientistas de dados na equipa de Machine Learning Olá, rapidamente fornecidas algumas dicas úteis. 

* Quando utiliza Olá [regressão Linear] [ linear-regression] módulo no Machine Learning Studio, dois métodos são fornecidos:
  * Online descendente de gradação: Pode ser mais adequada para problemas de grande escala
  * Comum de menos de quadrados: Este é o método Olá a maioria das pessoas encaram quando estes ouvir regressão linear. Para conjuntos de dados pequenos comum menos quadrados pode ser uma escolha ideal mais.
* Considere ajuste o desempenho de tooimprove Olá L2 Regularization ponderação parâmetro. Está definido too0.001 por predefinição, mas o nosso pequeno conjunto de dados definimos-too0.005 tooimprove desempenho. 

### <a name="mystery-solved"></a>Mystery resolvido!
Quando Aplicamos recomendações Olá, iremos conseguido Olá mesmo desempenho de linha de base no Machine Learning Studio, tal como acontece com o Excel: 

|  | Excel | Studio (inicial) | Studio com menos quadrados |
| --- |:---:|:---:|:---:|
| Valor identificado |Actuals (numérico) |mesmo |mesmo |
| Learner |Excel -> dados Analysis -> regressão |Regressão linear. |Regressão linear |
| Opções de learner |N/D |Predefinições |quadrados de menos comum<br />L2 = 0.005 |
| Conjunto de dados |26 linhas, 3 funcionalidades, 1 etiqueta. Todos os numérica. |mesmo |mesmo |
| Divisão: formação |Excel preparado no Olá primeiro 18 linhas, testado Olá pela última vez 8 linhas. |mesmo |mesmo |
| Divisão: teste |Excel fórmula de regressão aplicada toohello última 8 linhas |mesmo |mesmo |
| **Desempenho** | | | |
| Tendo em conta os parênteses de R |0.96 |N/D | |
| Coeficiente de determinação |N/D |0.78 |0.952049 |
| Tem de estar verdadeiramente erros absolutos |$9. 5M |$ 19.4 M |$9. 5M |
| Tem de estar verdadeiramente erros absolutos (%) |<span style="background-color: 00FF00;"> 6.03%</span> |12.2% |<span style="background-color: 00FF00;"> 6.03%</span> |

Além disso, coefficients de Excel Olá em comparação com bem toohello ponderações de funcionalidade em Olá modelo treinado do Azure:

|  | Excel Coefficients | Peso da funcionalidade do Azure |
| --- |:---:|:---:|
| Intercept/Bias |19470209.88 |19328500 |
| Funcionalidade A |0.832653063 |0.834156 |
| Funcionalidade B |11071967.08 |11007300 |
| Funcionalidade C |25383318.09 |25140800 |

## <a name="next-steps"></a>Passos Seguintes
Queremos que o serviço web do tooconsume Olá Machine Learning no Excel. Os nossos analistas de negócios baseiam-se no Excel e for necessário um Olá toocall de forma Machine Learning serviço com uma linha de dados do Excel web e o tiver devolver Olá prever valor tooExcel. 

Também queremos toooptimize nosso modelo, com opções de Olá e algoritmos disponíveis no Machine Learning Studio.

### <a name="integration-with-excel"></a>Integração com o Excel
A nossa solução era toooperationalize nosso regressão de Machine Learning modelo através da criação de um serviço web de modelo treinado Olá. Dentro de alguns minutos, o serviço de web de Olá foi criado e foi a que chamamos diretamente a partir do Excel tooreturn um valor previsto receitas. 

Olá *Dashboard de serviços Web* secção inclui um livro do Excel transferível. livro Olá inclui previamente formatado Olá web API e esquema de informações do serviço incorporadas. Ao clicar em *Transferir livro do Excel*, livro Olá abre e pode guardá-lo tooyour de computador local. 

![][1]

Com o livro Olá aberto, copie os parâmetros predefinidos na secção de parâmetro de Olá azul, conforme mostrado abaixo. Assim que são introduzidos parâmetros Olá, Excel chama toohello serviço web Machine Learning e hello previstas etiquetas classificadas serão apresentadas na secção de valores previstos Olá verde. livro Olá continuará toocreate predições para os parâmetros com base no seu modelo treinado para todos os itens de linha introduzidos em parâmetros. Para obter mais informações sobre como toouse esta funcionalidade, consulte [consumir um serviço de Web do Azure Machine Learning a partir do Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Otimização e mais experimentações
Agora que Tivemos uma linha de base com o nosso modelo do Excel, é movido toooptimize antecipada nosso modelo de regressão Linear do Machine Learning. Utilizámos o módulo Olá [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] tooimprove no nosso seleção de elementos de dados inicial e ajudou-na alcançar uma melhoria do desempenho de 4.6% significa erros absolutos. Para projetos futuros utilizaremos esta funcionalidade que foi possível guardar nos semanas no repetir dados atributos toofind Olá conjunto correto de funcionalidades toouse para modelling. 

Em seguida planeamos tooinclude algoritmos adicionais, como [Bayesiano] [ bayesian-linear-regression] ou [árvores de decisões elevada] [ boosted-decision-tree-regression] no nosso toocompare experimentação desempenho. 

Se quiser tooexperiment com regressão, tootry um bom conjunto de dados é Olá energia eficiência regressão exemplo conjunto de dados, que tem muitos dos atributos numéricos. conjunto de dados de Olá é fornecido como parte de conjuntos de dados de exemplo de Olá no Machine Learning Studio. Pode utilizar uma variedade de aprendizagem módulos toopredict Heating carga ou arrefecimento carga. gráfico de Olá abaixo é que uma comparação de desempenho de regressão diferentes aprende contra Olá eficiência energética dataset prever para Olá carga arrefecimento variável de destino: 

| Modelo | Tem de estar verdadeiramente erros absolutos | Erro ao quadrado de média de raiz | Erro relativo absoluto | Erro ao quadrado de caminho relativo | Coeficiente de determinação |
| --- | --- | --- | --- | --- | --- |
| Árvore de decisões elevada |0.930113 |1.4239 |0.106647 |0.021662 |0.978338 |
| Regressão linear (descendente gradação) |2.035693 |2.98006 |0.233414 |0.094881 |0.905119 |
| A rede neuronal regressão |1.548195 |2.114617 |0.177517 |0.047774 |0.952226 |
| Regressão linear (quadrados de menos comum) |1.428273 |1.984461 |0.163767 |0.042074 |0.957926 |

## <a name="key-takeaways"></a>Chaves Takeaways
Iremos aprendido muito por regressão de Excel em execução e experimentações do Azure Machine Learning em paralelo. Criar modelo de linha de base de Olá no Excel e comparando-toomodels com Machine Learning [regressão Linear] [ linear-regression] ajudou-nos obter o Azure Machine Learning e iremos detetados dados de tooimprove oportunidades desempenho de seleção e o modelo. 

Encontrámos também é aconselhável toouse [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] tooaccelerate projetos de predição futuras. Ao aplicar dados de tooyour de seleção de funcionalidade, pode criar um modelo melhorado no Machine Learning com um melhor desempenho global. 

Olá de tootransfer de capacidade de Olá preditiva analíticas previsão do Machine Learning tooExcel systemically permite que um aumento significativo na Olá capacidade toosuccessfully fornecer resultados público-alvo de utilizador do tooa abrangente de negócio. 

## <a name="resources"></a>Recursos
Seguem-se alguns recursos para ajudar a trabalhar com regressão: 

* Regressão no Excel. Se nunca tiver tentou regressão no Excel, este tutorial torna mais fácil: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Regressão vs de previsão. Tyler Chessman escrito um artigo de blogue explicar como toodo tempo previsão de série no Excel, que contém a descrição de um beginner boa de regressão linear. [http://sqlmag.com/SQL-Server-Analysis-Services/Understanding-Time-Series-forecasting-Concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Regressão Linear comum menos quadrados: Falhas, problemas e Pitfalls. Para uma introdução e debate de regressão: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

