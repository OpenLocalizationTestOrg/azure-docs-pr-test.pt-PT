---
title: desempenho do modelo de aaaEvaluate no Machine Learning | Microsoft Docs
description: Explica como tooevaluate modelo desempenho no Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Como tooevaluate modelo desempenho no Azure Machine Learning
Este artigo demonstra como tooevaluate Olá desempenho de um modelo no Azure Machine Learning Studio e fornece uma breve explicação de métricas de Olá disponíveis para esta tarefa. Três cenários comuns do learning supervisionado são apresentados: 

* Regressão
* classificação binária 
* classificação de várias classes

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Avaliar o desempenho de Olá de um modelo é uma das fases de núcleos de Olá no processo de ciência de dados de Olá. Indica como êxito Olá classificação (predições) de um conjunto de dados foi por um modelo preparado. 

Azure Machine Learning suporta a avaliação de modelo através de dois dos seu principal do machine learning módulos: [avaliar modelo] [ evaluate-model] e [modelo de validação cruzada][cross-validate-model]. Estes módulos permitem-lhe toosee como o seu modelo efetua em termos de um número de métricas que são frequentemente utilizadas no machine learning e estatísticas.

## <a name="evaluation-vs-cross-validation"></a>Avaliação vs. Validação de se estender
Avaliação e validação cruzada são desempenho de Olá toomeasure formas padrão do seu modelo. Podem ambos geram métricas de avaliação que pode verificar ou comparar relativamente aos outros modelos.

[Avaliar modelo] [ evaluate-model] espera um conjunto de dados classificado como entrada (ou 2 caso em que gostaria de desempenho de Olá toocompare de 2 modelos diferentes). Isto significa que terá de tootrain o modelo utilizando Olá [preparar modelo] [ train-model] predições do módulo e faça algumas conjunto de dados utilizando Olá [Pontuar modelo] [ score-model] módulo, antes de pode avaliar resultados Olá. Olá avaliação baseia-se no Olá classificada etiquetas/probabilidades juntamente com etiquetas verdadeiro Olá, todos os que são produzidas pelas Olá [Pontuar modelo] [ score-model] módulo.

Em alternativa, pode utilizar validação cruzada tooperform um número de avaliar de pontuação de formação operações (10 subconjuntos de validação) automaticamente em subconjuntos diferentes Olá de dados de entrada. dados de entrada Olá são divididos em 10 peças, onde um está reservado para fins de teste e Olá outros 9 para formação. Este processo é repetido 10 vezes e métricas de avaliação de Olá são uma média. Isto ajuda a determinar o quão bem um modelo seria generalizar toonew conjuntos de dados. Olá [modelo de validação cruzada] [ cross-validate-model] módulo aceita um modelo untrained e algumas assinalada como a 10 subconjuntos de validação de conjunto de dados e saídas Olá resultados da avaliação de cada uma das Olá, além disso toohello uma média de resultados.

No Olá secções a seguir, iremos criar modelos de regressão e classificação simples e avaliar o seu desempenho, utilizando os dois Olá [avaliar modelo] [ evaluate-model] e Olá [validação cruzada Modelo] [ cross-validate-model] módulos.

## <a name="evaluating-a-regression-model"></a>Avaliar um modelo de regressão
Assumir que queremos toopredict preço de um carro com algumas funcionalidades, tais como dimensões, potência de cavalos, especificações de motor e assim sucessivamente. Este é um problema de regressão típica, onde Olá variável de destino (*preços*) é um valor numérico contínuo. Iremos podem ajustar um modelo de regressão linear simples que, fornecido Olá funcionalidade valores de um carro determinadas pode prever preço Olá desse automóvel. Pode ser utilizado neste modelo de regressão tooscore Olá foi preparados no mesmo conjunto de dados. Assim que tiver hello os preços previstos para todos os carros Olá, iremos pode avaliar o desempenho de Olá do modelo de Olá observando quanto predições Olá desvio de preços real Olá em média. tooillustrate, utilizamos Olá *o conjunto de dados do automóvel preços dados (bruto)* disponíveis no Olá **conjuntos de dados guardado** secção no Azure Machine Learning Studio.

### <a name="creating-hello-experiment"></a>Criar Olá experimentação
Adicione Olá seguintes módulos tooyour área de trabalho do Azure Machine Learning Studio:

* Dados do preço automóvel (bruto)
* [Regressão linear][linear-regression]
* [Preparar modelo][train-model]
* [Modelo de pontuação][score-model]
* [Avaliar modelo][evaluate-model]

Ligar as portas de Olá, conforme mostrado abaixo na figura 1 e a etiqueta de conjunto de Olá colunas de Olá [preparar modelo] [ train-model] módulo demasiado*preços*.

![Avaliar um modelo de regressão](media/machine-learning-evaluate-model-performance/1.png)

Figura 1. Avaliar um modelo de regressão.

### <a name="inspecting-hello-evaluation-results"></a>A inspecionar o resultado da avaliação de Olá
Após a experimentação de Olá em execução, pode clicar na porta de saída de Olá de Olá [avaliar modelo] [ evaluate-model] módulo e selecione *visualizar* resultados da avaliação toosee Olá. Olá métricas de avaliação disponíveis para os modelos de regressão são: *significa erros absolutos*, *raiz a média dos erros absolutos*, *erro relativo absoluto*,  *Erro relativo ao quadrado*e Olá *coeficiente de determinação*.

termo Olá "error" aqui representa a diferença de Olá entre Olá valor previsto e o valor de true Olá. valor absoluto de Olá ou Olá quadrado desta diferença são geralmente calculadas toocapture Olá total prever a importância do erro em todas as instâncias, como a diferença de Olá entre Olá e valor verdadeiro pode ser negativo em alguns casos. métricas de erro Olá medem o desempenho de preditiva Olá de um modelo de regressão em termos de média de Olá desvio das respetivas predições de valores VERDADEIRO Olá. Valores mais baixos de erro significam Olá é mais exata tomar as predições. Uma métrica de erro geral de 0 significa que Olá modelo encaixa dados Olá perfeitamente.

coeficiente de Olá de determinação, que também é conhecido como R ao quadrado, também é uma forma de medir Olá quão bem modelo dados Olá padrão. Pode ser interpretado como proporção Olá da variação explicada por modelo de Olá. Um superior proporção é melhor neste caso, em que 1 indica uma opção perfeita.

![Métricas de avaliação de regressão linear](media/machine-learning-evaluate-model-performance/2.png)

Figura 2. Métricas de avaliação de regressão linear.

### <a name="using-cross-validation"></a>Utilizar cruzadas validação
Conforme mencionado anteriormente, pode realizar repetida formação, classificação e avaliações automaticamente utilizando Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Tudo o que precisa neste caso, é um conjunto de dados, um modelo untrained e um [modelo de validação cruzada] [ cross-validate-model] módulo (veja a figura abaixo). Tenha em atenção que tem de coluna de etiqueta de Olá tooset demasiado*preços* no Olá [modelo de validação cruzada] [ cross-validate-model] propriedades do módulo.

![Um modelo de regressão de validação cruzada](media/machine-learning-evaluate-model-performance/3.png)

Figura 3. Validação cruzada um modelo de regressão.

Após a experimentação de Olá em execução, pode inspecionar resultados da avaliação Olá clicando na porta de saída à direita Olá de Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Isto irá proporcionar uma vista detalhada das métricas de Olá para cada iteração (subconjuntos de validação) e Olá apresentou uma média de resultados de cada uma das métricas de Olá (figura 4).

![Resultados da validação cruzada de um modelo de regressão](media/machine-learning-evaluate-model-performance/4.png)

Figura 4. Resultados da validação cruzada de um modelo de regressão.

## <a name="evaluating-a-binary-classification-model"></a>Avaliar um modelo de classificação binária
Num cenário de classificação binária, variável de destino Olá tem apenas dois resultados possíveis, por exemplo: {0, 1} ou {FALSO, true}, {negativo, positivo}. Partem do princípio de que é-lhe fornecido um conjunto de dados de funcionários para adultos com algumas demográficos e variáveis da sua admissão e que é-lhe perguntado nível de receitas de Olá toopredict, uma variável binário com valores de Olá {"< = 50K", "> 50K"}. Por outras palavras, classe negativo Olá representa Olá empregados tornar menor ou igual too50K por ano e Olá positivo classe representa todos os outros empregados. Como no cenário de regressão Olá, vamos dar formação sobre um modelo, Pontuar alguns dados e, avaliar resultados Olá. Olá principal diferença aqui é a escolha de Olá de métricas que calcula do Azure Machine Learning e saídas. cenário de predição de nível de receitas de Olá tooillustrate, utilizaremos Olá [para adultos](http://archive.ics.uci.edu/ml/datasets/Adult) toocreate de conjunto de dados um Azure Machine Learning testar e avaliar o desempenho de Olá de um modelo de regressão logística da classe dois, um binário frequentemente utilizado classificador.

### <a name="creating-hello-experiment"></a>Criar Olá experimentação
Adicione Olá seguintes módulos tooyour área de trabalho do Azure Machine Learning Studio:

* Conjunto de dados de classificação binária de receitas Census para adultos
* [Regressão logística da duas classes][two-class-logistic-regression]
* [Preparar modelo][train-model]
* [Modelo de pontuação][score-model]
* [Avaliar modelo][evaluate-model]

Ligar as portas de Olá, conforme mostrado abaixo na figura 5 e o conjunto de Olá etiqueta colunas de Olá [preparar modelo] [ train-model] módulo demasiado*receitas*.

![Avaliar um modelo de classificação binária](media/machine-learning-evaluate-model-performance/5.png)

Figura 5. Avaliar um modelo de classificação binária.

### <a name="inspecting-hello-evaluation-results"></a>A inspecionar o resultado da avaliação de Olá
Após a experimentação de Olá em execução, pode clicar na porta de saída de Olá de Olá [avaliar modelo] [ evaluate-model] módulo e selecione *visualizar* resultados da avaliação toosee Olá (figura 7). Olá métricas de avaliação disponíveis para os modelos de classificação binária são: *precisão*, *precisão*, *recuperar*, *F1 pontuação*, e *AUC*. Além disso, o módulo Olá produz uma matriz de confusão, que mostra o número de Olá de positivos true, falsas negatives, falsos positivos e negatives verdadeiros, bem como *ROC*, *precisão/devolução de chamada*e *De comparação de precisão* curvas.

Precisão é simplesmente proporção de Olá de instâncias corretamente classificadas. Normalmente, é métrica primeiro Olá que observar quando um classificador a avaliar. No entanto, quando os dados de teste de Olá são desequilibrada (onde a maioria das instâncias de Olá pertence tooone das classes de Olá), ou é mais interessado no desempenho Olá uma das classes de Olá, exatidão realmente não captura eficácia Olá de um classificador. Cenário de nível de classificação de receitas Olá, partem do princípio de que está a testar em alguns dados em que 99% contra as instâncias de Olá representam as pessoas que mais significativos beneficiar de menor ou igual too50K por ano. É possível tooachieve uma precisão 0.99 ao prever classe Olá "< = 50K" para todas as instâncias. Neste caso, classificador de Olá aparece toobe fazer um bom trabalho geral, mas na realidade, falhar tooclassify qualquer uma das pessoas high-income de Olá (Olá 1%) corretamente.

Por esse motivo, é útil toocompute métricas adicionais que capturam aspetos mais específicos da avaliação de Olá. Antes de avançar para detalhes de Olá destas métricas, é importante toounderstand matriz de confusão Olá de uma avaliação de classificação binária. classe de Olá etiquetas no conjunto de preparação de Olá podem demorar em apenas 2 valores possíveis, que é normalmente Consulte tooas positivo ou negativo. Olá positivos e negativos as instâncias que um classificador prevê corretamente são denominadas positivos verdadeiros (TP) e negatives verdadeiros (TW), respetivamente. Da mesma forma, instâncias de Olá incorretamente classificado são denominadas falsos positivos (FP) e negatives falsos (FN). matriz de confusão Olá é simplesmente uma tabela que mostra o número de Olá de instâncias abrangidos por cada uma destas 4 categorias. O Azure Machine Learning automaticamente decide que de duas classes de Olá no conjunto de dados de Olá é classe positivo Olá. Se as etiquetas de classe Olá são Boolean ou números inteiros, em seguida, Olá instâncias com nome, 'true' ou '1' estão atribuídas a classe positivo Olá. Se as etiquetas de Olá são cadeias, como no caso de Olá de conjunto de dados de receitas de Olá, etiquetas Olá são ordenadas por ordem alfabética e nível primeiro Olá é escolhido classe negativo de Olá toobe enquanto o segundo nível de Olá é classe positivo Olá.

![Matriz de confusão de classificação binária](media/machine-learning-evaluate-model-performance/6a.png)

Figura 6. Matriz de confusão de classificação binária.

Retroceder toohello problema de classificação de receitas, seria queremos tooask várias perguntas de avaliação que ajudam-na compreender o desempenho de Olá do classificador de Olá utilizado. Uma pergunta muito natural é: ' fora indivíduos Olá quem Olá modelo toobe prevista earning > 50 K (TP + FP), quantas foram corretamente classificadas (TP)? " Esta questão pode ser respondida observando Olá **precisão** do modelo de Olá, que é a proporção Olá de positivos que estão corretamente classificados: TP/(TP+FP). Outra pergunta comum é "fora de todos os Olá elevada earning funcionários com receitas > 50 k (TP + FN), quantos Olá classificador classificar corretamente (TP)". Isto é, na verdade, Olá **recuperar**, ou a taxa de positivo verdadeiro Olá: TP/(TP+FN) do classificador de Olá. Poderá reparar que há um compromisso óbvios entre precisão e devolução de chamada. Por exemplo, atribuído um conjunto de dados relativamente equilibrado, um classificador que prevê principalmente positivas instâncias, teria uma devolução de chamada elevada, mas uma precisão em vez disso baixa como muitas das instâncias negativo Olá seria misclassified resultando num grande número de falsos positivos. gráfico de como estas duas métricas variam toosee, pode clicar em curva de ' Precisão/devolução de chamada' Olá na página de saída de resultado de avaliação de Olá (canto superior esquerdo parte da figura 7).

![Resultados da avaliação de classificação binária](media/machine-learning-evaluate-model-performance/7.png)

A figura 7. Resultados da avaliação de classificação binária.

Outro relacionadas com a métrica é frequentemente utilizada é Olá **F1 pontuação**, que demora a precisão e devolução de chamada em consideração. É Olá harmonic média destas métricas de 2 e é calculada como tal: F1 = 2 (devolução de chamada de precisão x) / (precisão + devolução de chamada). classificação de F1 Olá é uma avaliação de Olá toosummarize boa forma de várias único, mas é sempre toolook uma boa prática em precisão tanto devolução de chamada toobetter em conjunto compreender a forma como se comporta um classificador.

Além disso, um pode inspecionar taxa positivo verdadeiro Olá vs taxa positivo falso no Olá Olá **Recetor operativo característica (ROC)** curva e Olá correspondente **Olá área na curva (AUC)** valor. Olá próximo este curva toohello superior esquerda canto, desempenho do Olá melhor Olá classificador é (ou seja maximizando Olá Verdadeiro positivo taxa, para minimizar a taxa de positivo falso Olá). Curvas são toohello fechar diagonal de Olá desenho, resultado de classificadores tendem toomake predições que são fechar toorandom deteção.

### <a name="using-cross-validation"></a>Utilizar cruzadas validação
Exemplo de regressão Olá, iremos pode efetuar a validação cruzada toorepeatedly formação, Pontuar e avaliar diferentes subconjuntos de dados de Olá automaticamente. Da mesma forma, podemos utilizar Olá [modelo de validação cruzada] [ cross-validate-model] módulo, um modelo de regressão logística da untrained e um conjunto de dados. coluna de etiqueta Olá tem de ser definida demasiado*receitas* no Olá [modelo de validação cruzada] [ cross-validate-model] propriedades do módulo. Depois de executar a experimentação Olá e clicar no Olá direito de saída a porta da Olá [modelo de validação cruzada] [ cross-validate-model] módulo, é possível ver métrica de classificação binária Olá valores para cada subconjuntos de validação, além disso toohello média e o desvio-padrão de cada um. 

![Um modelo de classificação binária de validação cruzada](media/machine-learning-evaluate-model-performance/8.png)

Figura 8. Validação cruzada um modelo de classificação binária.

![Resultados da validação cruzada de um classificador binário](media/machine-learning-evaluate-model-performance/9.png)

Figura 9. Resultados da validação cruzada de um classificador binário.

## <a name="evaluating-a-multiclass-classification-model"></a>Avaliar um modelo de classificação de várias classes
Esta fase experimental utilizaremos Olá popular [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") conjunto de dados que contém instâncias das 3 diferentes tipos (classes) de maquinaria de iris Olá. Existem 4 funcionalidade valores (comprimento de sepal/largura e petal comprimento/largura) para cada instância. Nas experimentações anterior Olá preparado e modelos de Olá testado utilizando Olá mesmos conjuntos de dados. Aqui, utilizamos Olá [dividir dados] [ split] subconjuntos de toocreate 2 do módulo de dados de Olá, formação em Olá em primeiro lugar, Pontuar e avaliar em Olá segundo. Olá Iris dataset é publicamente disponível na Olá [UCI Machine Learning repositório](http://archive.ics.uci.edu/ml/index.html)e podem ser transferidos utilizando uma [importar dados] [ import-data] módulo.

### <a name="creating-hello-experiment"></a>Criar Olá experimentação
Adicione Olá seguintes módulos tooyour área de trabalho do Azure Machine Learning Studio:

* [Importar dados][import-data]
* [Floresta de decisão de várias classes][multiclass-decision-forest]
* [Dividir dados][split]
* [Preparar modelo][train-model]
* [Modelo de pontuação][score-model]
* [Avaliar modelo][evaluate-model]

Ligar as portas de Olá, conforme mostrado abaixo na figura 10.

Definir o índice de colunas de etiqueta Olá de Olá [preparar modelo] [ train-model] too5 do módulo. conjunto de dados de Olá não tem nenhuma linha de cabeçalho, mas sabemos dessa classe Olá as etiquetas são Olá quinta coluna.

Clique em Olá [importar dados] [ import-data] módulo e conjunto Olá *origem de dados* propriedade demasiado*URL da Web através de HTTP*e Olá *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Conjunto Olá fração de toobe de instâncias utilizado para formação em Olá [dividir dados] [ split] módulo (0,7 por exemplo).

![Avaliar um classificador de várias classes](media/machine-learning-evaluate-model-performance/10.png)

A figura 10. Avaliar um classificador de várias classes

### <a name="inspecting-hello-evaluation-results"></a>A inspecionar o resultado da avaliação de Olá
Execute experimentação Olá e clique na porta de saída de Olá do [avaliar modelo][evaluate-model]. resultados da avaliação Olá são apresentados no formato Olá uma matriz de confusão, neste caso. matriz de Olá mostra Olá real vs instâncias previstas para todas as classes de 3.

![Resultados da avaliação de classificação de várias classes](media/machine-learning-evaluate-model-performance/11.png)

Figura 11. Resultados da avaliação de classificação de várias classes.

### <a name="using-cross-validation"></a>Utilizar cruzadas validação
Conforme mencionado anteriormente, pode realizar repetida formação, classificação e avaliações automaticamente utilizando Olá [modelo de validação cruzada] [ cross-validate-model] módulo. Terá de um conjunto de dados, um modelo untrained e um [modelo de validação cruzada] [ cross-validate-model] módulo (veja a figura abaixo). Novamente terá tooset Olá etiqueta coluna Olá [modelo de validação cruzada] [ cross-validate-model] módulo (índice de coluna de 5 neste caso). Depois de executar a experimentação Olá e clicando em direito Olá saída porta de Olá [modelo de validação cruzada][cross-validate-model], pode inspecionar os valores de métrica de Olá para cada fold, bem como Olá média e o desvio-padrão. métricas de Olá apresentadas aqui são Olá semelhante toohello aqueles abordado no caso de classificação binária Olá. No entanto, tenha em atenção que numa classificação várias classes, informática Olá verdadeiro positivos/negatives e falsos positivos/negatives é efetuado por contando numa base por classe, tal como não é não existe nenhuma classe geral positivo ou negativo. Por exemplo, quando informático precisão de Olá ou devolução de chamada de Olá 'Iris setosa' classe, presume-se que se trata classe positivo Olá e todos os outros como negativo.

![Um modelo de classificação de várias classes de validação cruzada](media/machine-learning-evaluate-model-performance/12.png)

Figura 12. Validação cruzada um modelo de classificação de várias classes.

![Resultados da validação cruzada de um modelo de classificação de várias classes](media/machine-learning-evaluate-model-performance/13.png)

Figura 13. Resultados da validação cruzada de um modelo de classificação de várias classes.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

