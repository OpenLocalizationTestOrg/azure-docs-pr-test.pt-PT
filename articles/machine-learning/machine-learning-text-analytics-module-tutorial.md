---
title: "modelos de análise de texto aaaCreate no Azure Machine Learning Studio | Microsoft Docs"
description: "Como a análise de texto toocreate modelos no Azure Machine Learning Studio com módulos de texto pré-processamentos, N-grams ou funcionalidade hash"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Criar modelos de análise de texto no Azure Machine Learning Studio
Pode utilizar o Azure Machine Learning toobuild e operacionalizar modelos de análise de texto. Estes modelos podem ajudar a resolver, por exemplo, problemas de análise de classificação de recursos de dados de sentimento do documento.

Numa experimentação da análise de texto, normalmente, seria:

1. Limpar e processar previamente os do conjunto de dados de texto
2. Extrair vetores de funcionalidade numérico a partir de texto de pré-processado
3. Preparar modelo de classificação ou regressão
4. Pontuar e valide o modelo de Olá
5. Implementar Olá modelo tooproduction

Neste tutorial, aprende estes passos, iremos guiá-lo através de um modelo de análise de dados de sentimento utilizando o conjunto de dados do Amazon livro revisões (consulte neste documento research "Biographies, Bollywood, caixas de Boom e Blenders: Adaptation de domínio para classificação de dados de sentimento" pelo João Blitzer, Marcar Dredze e Fernando Pereira; Associação de Linguistics computacional (ACL), 2007.) Este conjunto de dados é constituído por pontuações de revisão (1-2 ou 4 a 5) e um texto livre. Olá objetivo é pontuação de revisão de Olá toopredict: baixa (1 - 2) ou elevado (4-5).

Pode encontrar experimentações abrangidas neste tutorial na galeria da Cortana Intelligence:

[Prever revisões de livro](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Prever livro revisões - experimentação preditiva](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>Passo 1: Limpar e processar previamente os do conjunto de dados de texto
Iremos começar Olá experimentação dividindo pontuações de revisão Olá problema de Olá tooformulate categórico registos baixa e alta como a classificação de duas classes. Utilizamos [Editar metadados](https://msdn.microsoft.com/library/azure/dn905986.aspx) e [valores Categórico grupo](https://msdn.microsoft.com/library/azure/dn906014.aspx) módulos.

![Criar etiqueta](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Em seguida, iremos limpar Olá texto utilizando [processar previamente os texto](https://msdn.microsoft.com/library/azure/mt762915.aspx) módulo. limpeza de Olá reduz o ruído de Olá no conjunto de dados de Olá, Olá, ajuda a determinar Olá funcionalidades mais importantes e melhorar a precisão do modelo final Olá. Removemos palavras de paragem - palavras comuns, tais como "a" ou "a" - e números, carateres especiais, carateres de duplicados, endereços de correio eletrónico e URLs. Podemos também converter Olá texto toolowercase, lemmatize palavras Olá e detetar limites de frases que, em seguida, são indicados por "|||" símbolo texto pré-processado.

![Processar previamente os texto](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

E se pretende toouse uma lista personalizada de palavras de paragem? Pode passá-lo na como entrada opcional. Também pode utilizar personalizadas c# sintaxe expressão regular tooreplace subcadeias e remover palavras por parte de voz: substantivos, verbos ou adjectives.

Depois de concluída a pré-processamentos Olá, iremos dividir os dados de Olá em formação e teste conjuntos.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>Passo 2: Extrair vetores de funcionalidade numérico a partir de texto de pré-processado
toobuild um modelo de dados de texto, normalmente, terá de texto de forma livre tooconvert para vetores de funcionalidade numérico. Neste exemplo, utilizamos [extrair N grama as funcionalidades do texto](https://msdn.microsoft.com/library/azure/mt762916.aspx) módulo tootransform Olá dados toosuch o formato texto. Este módulo executa uma coluna de valores separados por espaços em branco palavras e calcula um dicionário de palavras ou N-grams de palavras, o que aparecem no seu conjunto de dados. Em seguida, contagens quantas vezes cada word ou N-grama, é apresentado em cada registo e cria os vetores de funcionalidade das contagem. Neste tutorial, definimos grama N tamanho too2, pelo que o nosso vetores de funcionalidade incluem palavras único e combinações de duas palavras subsequentes.

![Extrair N-grams](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Iremos aplicar TF * IDF (termo frequência inverso documento frequência) weighting tooN grama contagens. Esta abordagem adiciona uma ponderação de palavras que aparecem frequentemente num único registo, mas são raro em todo Olá de conjunto de dados. Outras opções incluem binary, TF e graph weighing.

Estas funcionalidades de texto, muitas vezes, têm dimensionalidades elevada. Por exemplo, se a sua corpus tiver 100 000 palavras exclusivas, o espaço de funcionalidade teria 100.000 dimensões ou mais se N-grams são utilizados. módulo de funcionalidades de N grama extrair Olá dá-lhe um conjunto de dimensionalidade de Olá tooreduce de opções. Pode escolher tooexclude palavras que são valor preditiva significativas de toohave curto ou longo ou demasiado invulgar ou demasiado frequente. Neste tutorial, iremos excluir N-grams que são apresentados em menos de 5 registos ou em mais de 80% dos registos.

Além disso, pode utilizar tooselect de seleção de funcionalidade apenas essas funcionalidades que são mais Olá correlacionadas com o destino de predição. Utilizamos funcionalidades de 1000 de tooselect de seleção de funcionalidade de qui-quadrado. Pode ver vocabulário Olá de palavras selecionadas ou N-grams clicando saída à direita do Olá do módulo de extrair N-grams.

Como toousing extrair funcionalidades de N grama uma abordagem alternativa, pode utilizar o módulo de funcionalidade hash. Tenha em atenção que que [funcionalidade hash](https://msdn.microsoft.com/library/azure/dn906018.aspx) não possui capacidades de seleção de funcionalidade em compilação ou TF * IDF weighing.

## <a name="step-3-train-classification-or-regression-model"></a>Passo 3: Preparar o modelo de classificação ou regressão
Agora, texto Olá foi toonumeric transformados funcionalidade colunas. conjunto de dados de Olá ainda contém colunas de cadeia de fases anteriores, pelo que iremos utilizar selecionar colunas no conjunto de dados tooexclude-los.

Em seguida, utilizamos [duas classes de regressão logística da](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict nosso destino: pontuação de revisão elevada ou baixa. Neste momento, o problema de análise de texto Olá ter sido transformado um problema de classificação regular. Pode utilizar as ferramentas de Olá disponíveis no modelo do Azure Machine Learning tooimprove Olá. Por exemplo, pode experimentar diferentes classificadores toofind os resultados como precisos conceder ou utilizar hyperparameter precisão de Olá tooimprove de otimização.

![Formação e Pontuar](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>Passo 4: Pontuar e valide o modelo de Olá
Como pretende validar o modelo treinado Olá? Iremos pontuá-lo contra o conjunto de dados de teste de Olá e avaliar exatidão Olá. No entanto, o modelo de Olá aprendidas vocabulário Olá de N-grams e as respetivas importâncias do conjunto de dados de formação de Olá. Por conseguinte, que devemos utilizar essa vocabulário e uma dessas ponderações quando funcionalidades de dados de teste, a extrair como opposed vocabulário de Olá toocreating anew. Por conseguinte, iremos adicionar funcionalidades de N grama extrair o módulo toohello classificação ramo da experimentação Olá, ligar Olá vocabulário de saída do ramo de preparação e definir o modo de vocabulário Olá só tooread. Podemos também desativar Olá a filtragem de N-grams pela frequência por definição instância do Olá too1 mínimo e máximo too100% e desativar a seleção de funcionalidades Olá.

Depois de Olá coluna de texto no teste dados transformados toonumeric colunas de funcionalidade, iremos excluir cadeia Olá colunas de fases anteriores, como no ramo de preparação. Em seguida, utilizamos toomake predições do modelo de pontuação módulo e a precisão do modelo de avaliação módulo tooevaluate Olá.

## <a name="step-5-deploy-hello-model-tooproduction"></a>Passo 5: Implementar Olá modelo tooproduction
modelo de Olá está quase pronto toobe implementado tooproduction. Quando implementado como um serviço web, que demora a cadeia de texto de forma livre como entrada e devolver uma predição "Alta" ou "baixa". Utiliza Olá aprendida N grama vocabulário tootransform Olá texto toofeatures e preparado o modelo de regressão logística da toomake uma predição a partir dessas funcionalidades. 

tooset segurança experimentação preditiva Olá, vamos primeiro guarde vocabulário de N grama Olá como conjunto de dados e Olá preparado modelo de regressão logística do ramo de preparação de Olá da experimentação Olá. Em seguida, iremos guardar experimentação Olá "Guardar como" toocreate a utilizar um gráfico de experimentação para experimentação preditiva. Remover o módulo de dados de divisão de Olá e ramo de preparação de Olá experimentação Olá. Mas, em seguida, ligar Olá guardado anteriormente N grama vocabulário e modelo tooExtract N grama funcionalidades e os módulos do modelo de pontuação, respetivamente. Também Iremos remover o módulo de modelo de avaliação de Olá.

Iremos selecionar colunas de inserção de módulo de conjunto de dados antes de coluna de etiqueta do texto processar previamente os módulo tooremove Olá e anule a seleção de opção "Toodataset de coluna de modelo de pontuação de acréscimo" no módulo de pontuação. Dessa forma, Olá web não pedido de serviço etiqueta Olá que está a tentar toopredict e não escreverá funcionalidades de entrada Olá na resposta.

![Experimentação preditiva](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Agora que temos uma experimentação que pode ser publicada como um serviço web e chamada utilizando a execução do pedido-resposta ou lote APIs.

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre o módulos de análise de texto de [documentação MSDN](https://msdn.microsoft.com/library/azure/dn905886.aspx).

