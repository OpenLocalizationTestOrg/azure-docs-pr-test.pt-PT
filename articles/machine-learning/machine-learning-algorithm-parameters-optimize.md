---
title: aaaOptimize os algoritmos no Azure Machine Learning | Microsoft Docs
description: "Explica como parâmetro ideal de Olá toochoose definido para um algoritmo no Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Escolher os algoritmos de parâmetros toooptimize no Azure Machine Learning
Este tópico descreve como toochoose Olá direita hyperparameter definido para um algoritmo no Azure Machine Learning. A maioria dos algoritmos do machine learning tem tooset de parâmetros. Quando preparar um modelo, terá de valores de tooprovide para esses parâmetros. efficacy Olá de modelo treinado Olá depende de parâmetros de modelo de Olá que escolher. Olá processo de localizar o conjunto de ideal Olá de parâmetros é conhecido como *modelo seleção*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Existem várias seleção do modelo de toodo formas. No machine learning, validação cruzada é um dos métodos de Olá amplamente utilizado para a seleção do modelo e é o mecanismo de seleção do Olá predefinido modelo no Azure Machine Learning. Como o Azure Machine Learning suporta o R e Python, sempre que pode implementar os seus próprios mecanismos de seleção de modelo ao utilizar o R ou Python.

Existem quatro passos no processo de Olá de encontrar o conjunto de parâmetros melhor Olá:

1. **Definir o espaço de parâmetro de Olá**: para o algoritmo de Olá, primeiro tem de decidir valores de parâmetro exato de Olá pretende tooconsider.
2. **Definir as definições de validação cruzada Olá**: decidir como validação cruzada toochoose subconjuntos de validação para Olá conjunto de dados.
3. **Definir a métrica de Olá**: decida que toouse métrica para determinar o conjunto de melhor Olá de parâmetros, tais como a precisão, a média de raiz ao quadrado erro, precisão, devolução de chamada ou pontuação f.
4. **Preparar, avaliar e comparar**: para cada combinação de valores de parâmetro de Olá exclusivos, validação cruzada é realizada por e com base numa métrica de erro de Olá definir. Após a avaliação e comparação, pode escolher modelo best-realizar Olá.

Olá imagem a seguir ilustra mostra como este pode ser obtida no Azure Machine Learning.

![Localizar o conjunto de parâmetros melhor Olá](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Definir o espaço de parâmetro de Olá
Pode definir o parâmetro de Olá definido no passo de inicialização do modelo de Olá. Olá painel parâmetro de todos os algoritmos do machine learning tem dois modos de trainer: *único parâmetro* e *parâmetro intervalo*. Escolha o modo de intervalo de parâmetro. No modo de intervalo de parâmetro, pode introduzir vários valores para cada parâmetro. Pode introduzir valores separados por vírgulas na caixa de texto Olá.

![Árvore de decisões elevada de duas classes, parâmetro único](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Em alternativa, pode definir pontos de máxima e mínima de Olá de grelha Olá e o número total de Olá de toobe pontos gerada com **utilize intervalo Builder**. Por predefinição, os valores de parâmetros de Olá são gerados uma escala linear. Mas se **registo escala** estiver marcada, os valores de Olá são gerados no dimensionamento de registo Olá (ou seja, é constante em vez dos respetivos diferença rácio Olá dos pontos adjacentes Olá). Para os parâmetros de número inteiro, pode definir um intervalo utilizando um hífen. Por exemplo, "1-10" significa que todos os números inteiros entre 1 e 10 (ambos inclusivo) de forma Olá conjunto de parâmetros. O modo misto também é suportado. Por exemplo, Olá conjunto de parâmetros "1 a 10, 20, 50" inclui números inteiros 1 a 10, 20 e 50.

![Árvore de decisões elevada de duas classes, intervalo de parâmetro](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Definir subconjuntos de validação de validação cruzada
Olá [partição e amostras] [ partition-and-sample] módulo pode ser utilizado toorandomly atribuir subconjuntos de validação toohello dados. Olá a seguinte configuração de exemplo para o módulo Olá, iremos definir subconjuntos de validação de cinco e atribuir aleatoriamente um subconjunto de validação instâncias de exemplo toohello número.

![Partição e amostras](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Definir a métrica de Olá
Olá [modelo de sintonização] [ tune-model-hyperparameters] módulo fornece suporte para escolher empirically Olá conjunto melhor de parâmetros para um determinado algoritmo e o conjunto de dados. Além disso tooother informações relativas a formação Olá modelo, hello **propriedades** painel deste módulo inclui métrica Olá para determinar o conjunto de parâmetros melhor Olá. Tem duas caixas de diferentes na lista pendente para classificação e regressão algoritmos, respetivamente. Se o algoritmo de Olá em consideração é um algoritmo de classificação, a métrica de regressão Olá é ignorada e vice-versa. Neste exemplo específica, é métrica Olá **precisão**.   

![Parâmetros de paramétrico](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Preparar, avaliar e comparar
Olá mesmo [modelo de sintonização] [ tune-model-hyperparameters] módulo trains todos os modelos de Olá que correspondem o conjunto de parâmetros toohello, avalia várias métricas e, em seguida, cria o modelo best-treinado Olá com base no Olá métrica que escolher. Este módulo tem duas entradas obrigatórias:

* learner untrained Olá
* Olá conjunto de dados

módulo Olá tem também um conjunto de dados opcional de entrada. Ligar Olá conjunto de dados com informações de subconjuntos de validação toohello informações de conjunto de dados obrigatórios. Se o conjunto de dados de Olá não está atribuído a quaisquer informações de subconjuntos de validação, em seguida, uma validação cruzada 10-fold é executada automaticamente por predefinição. Se a atribuição de subconjuntos de validação de Olá não é efetuada e um conjunto de dados de validação é fornecido na porta de conjunto de dados opcional Olá, em seguida, é escolhido um modo de teste de formação e Olá primeiro conjunto de dados é o modelo de Olá de tootrain utilizado para cada combinação de parâmetro.

![Classificador de árvore de decisões elevada](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

modelo de Olá, em seguida, é avaliado no conjunto de dados de validação de Olá. Olá deixados porta de saída do mostra de módulo Olá métricas diferentes com as funções de valores de parâmetros. Olá à direita de porta de saída fornece modelo treinado Olá que corresponde ao modelo best-realizar toohello toohello escolhido métrica de acordo com (**precisão** neste caso).  

![Conjunto de dados de validação](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Pode ver parâmetros exato Olá escolhidos por visualizar Olá à porta de saída à direita. Este modelo pode ser utilizado na classificação de um conjunto de teste ou em serviços web operacionalizado depois de guardar como um modelo preparado.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
