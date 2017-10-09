---
title: "Passo 4: Preparar e avaliar os modelos de Análise Preditiva Olá | Microsoft Docs"
description: "Passo 4 do Olá desenvolver uma solução preditiva explicação passo a passo: preparar, Pontuar e avaliar vários modelos no Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Instruções passo 4: Preparar e avaliar os modelos de Análise Preditiva Olá
Este tópico contém quarto passo de Olá instruções Olá, [desenvolver uma solução de Análise Preditiva no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Criar uma área de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Carregar os dados existentes](machine-learning-walkthrough-2-upload-data.md)
3. [Criar uma nova experimentação](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Dar formação e avaliar os modelos de Olá**
5. [Implementar o serviço Web de Olá](machine-learning-walkthrough-5-publish-web-service.md)
6. [Aceder ao serviço Web Olá](machine-learning-walkthrough-6-access-web-service.md)

- - -
Uma das vantagens de Olá da utilização do Azure Machine Learning Studio para criar modelos de machine learning é Olá capacidade tootry mais do que um tipo de modelo de um momento a uma único experimentação e comparar os resultados de Olá. Este tipo de experimentação ajuda-o a determinar a melhor solução de Olá para o seu problema.

Na experimentação de Olá, iremos estiver a desenvolver esta explicação passo a passo, vamos criar dois tipos diferentes de modelos e, em seguida, compare os respetivos toodecide de resultados de classificação que algoritmo queremos toouse na nossa experimentação final.  

Existem vários modelos, pode escolher a partir do. modelos de Olá toosee disponíveis, expanda Olá **Machine Learning** nó na paleta do módulo Olá e, em seguida, expanda **inicializar modelo** e Olá nós que está abaixo. Para efeitos Olá esta fase experimental, iremos selecionar Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] (SVM) e Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulos.    

> [!TIP]
> Ajuda tooget decidir o algoritmo do Machine Learning que melhor se adequa aos problema específico Olá que está a tentar toosolve, consulte [como algoritmos toochoose do Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Formação Olá modelos

Vamos adicionar ambos os Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo e [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo deste experimentação.

### <a name="two-class-boosted-decision-tree"></a>Árvore de decisões elevada de duas classes

Em primeiro lugar, vamos configurar modelo de árvore de decisão Olá elevada.

1. Determinar Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo na paleta do módulo Olá e arraste-o para a tela Olá.

2. Determinar Olá [preparar modelo] [ train-model] módulo, arraste-o para a tela Olá e, em seguida, ligue resultado Olá Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree]módulo toohello deixado porta de entrada de Olá [preparar modelo] [ train-model] módulo.
   
   Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico Olá e [preparar modelo] [ train-model] utiliza dados de formação modelo de Olá tootrain. 

3. Ligar a saída à esquerda do Olá da esquerda Olá [executar Script do R] [ execute-r-script] porta de Olá de entrada do módulo toohello direito [preparar modelo] [ train-model] módulo (Iremos decidiu no [passo 3](machine-learning-walkthrough-3-create-new-experiment.md) destes instruções toouse Olá dados provenientes de Olá à esquerda do lado do módulo de dividir dados Olá para formação).
   
   > [!TIP]
   > Já não precisamos duas das entradas de Olá e uma das saídas de Olá da Olá [executar Script do R] [ execute-r-script] módulo para esta fase experimental, pelo que iremos pode deixá-los desanexados. 
   > 
   > 

Esta parte da experimentação Olá agora aspeto semelhante ao seguinte:  

![Um modelo de preparação][1]

Agora precisamos tootell Olá [preparar modelo] [ train-model] módulo que pretende é que o valor do Olá modelo toopredict Olá risco de crédito.

1. Selecione Olá [preparar modelo] [ train-model] módulo. No Olá **propriedades** painel, clique em **Seletor de coluna**.

2. No Olá **Selecione uma coluna** caixa de diálogo, escreva "risco de crédito" no campo de pesquisa de Olá em **colunas disponíveis**, selecione "Risco de crédito" abaixo e clique no botão de seta para a direita Olá ( **>** ) toomove "De crédito risco" demasiado**colunas selecionadas**. 

    ![Selecionar coluna de risco de crédito Olá para o módulo de modelo de formação Olá][0]

3. Clique em Olá **OK** marca de verificação.

### <a name="two-class-support-vector-machine"></a>Máquina de Vetores de Suporte de Duas Classes

Em seguida, iremos configurar modelo SVM Olá.  

Primeiro, um pequeno explicação sobre SVM. Árvores de decisões elevada funcionam bem com funcionalidades de qualquer tipo. No entanto, uma vez que o módulo SVM Olá gera um classificador linear, modelo de Olá gera tem Olá melhor teste erro quando todas as funcionalidades numérico têm Olá mesma escala. tooconvert numérico todas as funcionalidades toohello mesmo dimensionar, utilizamos uma transformação "Tanh" (com Olá [normalizar dados] [ normalize-data] módulo). Isto transforma nosso números em intervalo Olá [0,1]. módulo SVM Olá converte cadeia funcionalidades toocategorical, em seguida, toobinary 0/1 e das funcionalidades e, pelo que não suportamos necessário toomanually transformar funcionalidades de cadeia. Além disso, não queremos tootransform Olá risco de crédito coluna (21) - é numérico, mas não o valor de Olá que está a formação Olá toopredict de modelo, pelo que temos tooleave-lo individualmente.  

tooset segurança modelo SVM Olá Olá seguintes:

1. Determinar Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo na paleta do módulo Olá e arraste-o para a tela Olá.

2. Contexto Olá [preparar modelo] [ train-model] módulo, selecione **cópia**e, em seguida, faça duplo clique tela Olá e selecione **colar**. Olá cópia Olá [preparar modelo] [ train-model] Olá do módulo é mesmo seleção de coluna como Olá original.

3. Ligar o resultado Olá Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo toohello deixado porta de entrada de Olá segundo [preparar modelo] [ train-model] módulo.

4. Determinar Olá [normalizar dados] [ normalize-data] módulo e arraste-o para a tela Olá.

5. Ligar a saída à esquerda do Olá da esquerda Olá [executar Script do R] [ execute-r-script] entrada do módulo toohello deste módulo (tenha em atenção que Olá porta de saída de um módulo pode ser ligado toomore do que um outro módulo).

6. Ligar Olá deixado porta de saída do Olá [normalizar dados] [ normalize-data] módulo toohello direito de entrada a porta da Olá segundo [preparar modelo] [ train-model] módulo.

Esta parte do nosso experimentação deve agora algo semelhante ao seguinte:  

![Modelo de segundo formação Olá][2]  

Configurar agora Olá [normalizar dados] [ normalize-data] módulo:

1. Clique em tooselect Olá [normalizar dados] [ normalize-data] módulo. No Olá **propriedades** painel, selecione **Tanh** para Olá **método de transformação** parâmetro.

2. Clique em **Seletor de coluna**, selecione "Colunas" para **começar com**, selecione **incluir** no Olá primeira lista pendente, selecione **tipo da coluna**no Olá segundo pendente e selecione **numérico** na lista pendente de terceiro Olá. Esta ação Especifica que todos os Olá colunas numéricas (e apenas numérica) são transformados.

3. Clique em Olá toohello sinal de adição (+) à direita desta linha - esta ação cria uma linha com as dropdowns. Selecione **excluir** no Olá primeira lista pendente, selecione **os nomes das colunas** no Olá segundo pendente e introduza "Risco de crédito" no campo de texto Olá. Esta ação especifica essa coluna do risco de crédito Olá deve ser ignorada (temos toodo Isto porque esta coluna é numérico e por isso, deverá ser transformado se podemos não excluí-lo).

4. Clique em Olá **OK** marca de verificação.  

    ![Selecionar colunas para o módulo de dados normalizar Olá][5]

Olá [normalizar dados] [ normalize-data] módulo está agora conjunto tooperform uma transformação Tanh em todas as colunas numérico, exceto para a coluna de risco de crédito Olá.  

## <a name="score-and-evaluate-hello-models"></a>Pontuar e avaliar os modelos de Olá

Utilizamos Olá testar os dados que foi separados por Olá [dividir dados] [ split] módulo tooscore nosso modelos de formação. Vamos, em seguida, pode comparar Olá os resultados da Olá dois modelos toosee que gerados melhores resultados.  

### <a name="add-hello-score-model-modules"></a>Adicione módulos do modelo de pontuação de Olá

1. Determinar Olá [Pontuar modelo] [ score-model] módulo e arraste-o para a tela Olá.

2. Ligar Olá [preparar modelo] [ train-model] módulo que estabeleceu toohello [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] entrada à esquerda do módulo toohello porta de Olá [Pontuar modelo] [ score-model] módulo.

3. Ligar o direito de Olá [executar Script do R] [ execute-r-script] porta de Olá de entrada do módulo (nossos dados de teste) toohello direito [Pontuar modelo] [ score-model] módulo.

    ![Módulo do modelo de pontuação ligado][6]
   
   Olá [Pontuar modelo] [ score-model] módulo agora pode demorar informações de crédito Olá de Olá testar dados, executados-o utilizando o modelo de Olá, e os riscos de crédito predições de Olá comparar modelo Olá gera com Olá real coluna na Olá dados de teste.

4. Copie e cole Olá [Pontuar modelo] [ score-model] módulo toocreate uma segunda cópia.

5. Ligar a saída de Olá do modelo SVM hello (ou seja, Olá saída porta de Olá [preparar modelo] [ train-model] módulo que estabeleceu toohello [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo) toohello entrada porta de Olá segundo [Pontuar modelo] [ score-model] módulo.

6. Para o modelo SVM Olá, temos de toodo Olá mesmos dados de teste de transformação toohello como foi feito toohello dados de preparação. Por isso, copie e cole Olá [normalizar dados] [ normalize-data] módulo toocreate uma segunda cópia e ligue-o direito de toohello [executar Script do R] [ execute-r-script] módulo.

7. Ligar a saída à esquerda do Olá de Olá segundo [normalizar dados] [ normalize-data] módulo toohello direito de entrada a porta da Olá segundo [Pontuar modelo] [ score-model] módulo.

    ![Ambos os módulos de modelo de pontuação ligados][7]

### <a name="add-hello-evaluate-model-module"></a>Adicionar módulo do modelo de avaliação de Olá

tooevaluate Olá resultados de classificação dois e compará-los, utilizamos uma [avaliar modelo] [ evaluate-model] módulo.  

1. Determinar Olá [avaliar modelo] [ evaluate-model] módulo e arraste-o para a tela Olá.

2. Ligar a porta de saída de Olá do Olá [Pontuar modelo] [ score-model] módulo associado Olá elevada decisão toohello do modelo de árvore à esquerda de entrada a porta da Olá [avaliar modelo] [ evaluate-model] módulo.

3. Ligar Olá outro [Pontuar modelo] [ score-model] porta de entrada do módulo toohello à direita.  

    ![Avaliar modelo módulo ligado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Execute experimentação Olá e Olá resultados da verificação

toorun Olá experimentação, clique em Olá **executar** no botão abaixo tela Olá. Pode demorar alguns minutos. Mostra um indicador de girar em cada módulo que está a ser executado e, em seguida, uma marca de verificação verde mostra quando o módulo Olá estiver concluído. Quando todos os módulos de Olá têm uma marca de verificação, experimentação Olá concluiu a execução.

experimentação Olá deve agora algo semelhante ao seguinte:  

![Avaliar ambos os modelos][3]

resultados de Olá toocheck, clique em Olá porta de saída de Olá [avaliar modelo] [ evaluate-model] módulo e selecione **visualizar**.  

Olá [avaliar modelo] [ evaluate-model] módulo produz um par de curvas e métricas que lhe permitem resultados de Olá toocompare dos dois modelos de classificadas Olá. Pode ver os resultados de Olá como curvas Recetor operador característica (ROC), curvas precisão/devolução de chamada ou curvas de comparação de precisão. Dados adicionais apresentados incluem uma matriz de confusão, cumulativos valores para a área de Olá em curva de Olá (AUC) e outras métricas. Pode alterar o valor de limiar de Olá ao mover Olá o controlo de deslize esquerdo ou direito e ver como que isso afeta o conjunto de Olá de métricas.  

toohello à direita do gráfico de Olá, clique em **classificada dataset** ou **classificada toocompare de conjunto de dados** toohighlight Olá associado curva e toodisplay Olá associados métricas abaixo. Legenda de Olá para curvas Olá, "Classificada o conjunto de dados" corresponde toohello deixado porta de entrada de Olá [avaliar modelo] [ evaluate-model] módulo - no nosso caso, este é o modelo de árvore de decisão Olá elevada. "Classificada toocompare de conjunto de dados" corresponde a porta de entrada à direita toohello - modelo SVM Olá no nosso caso. Quando clica destas etiquetas, curva Olá para esse modelo é realçada e métricas correspondente Olá são apresentadas, conforme mostrado no Olá gráfico a seguir.  

![Curvas ROC para modelos][4]

Ao examinar estes valores, pode decidir o modelo está mais próximo toogiving que Olá resultados que procura. Pode voltar atrás e iterar sua experimentação, alterando os valores de parâmetros em modelos diferentes Olá. 

Ciência Olá e art de interpretar estes resultados e otimização de desempenho do modelo de Olá é exteriores Olá âmbito destas instruções. Para obter ajuda adicional, pode ler Olá seguintes artigos:
- [Como tooevaluate modelo desempenho no Azure Machine Learning](machine-learning-evaluate-model-performance.md)
- [Escolher os algoritmos de parâmetros toooptimize no Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md)
- [Interpretar os resultados de modelo no Azure Machine Learning](machine-learning-interpret-model-results.md)

> [!TIP]
> Sempre que executar a experimentação Olá um registo desse iteração é mantido no histórico de execuções de Olá. Pode ver estes iterações e devolver tooany dos mesmos, clicando **ver histórico de EXECUÇÕES** abaixo tela Olá. Também pode clicar em **executar o anterior** no Olá **propriedades** iteração toohello tooreturn de painel imediatamente anterior Olá um tiver aberto.
> 
> Pode efetuar uma cópia de qualquer iteração da sua experimentação, clicando em **guardar como** abaixo tela Olá. 
> Utilize a experimentação de Olá **resumo** e **Descrição** propriedades tookeep um registo das quais já tentou no seu iterações de experimentação.
> 
> Para obter mais detalhes, consulte [gerir iterações de experimentação no Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Seguinte: [implementar o serviço web de Olá](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
