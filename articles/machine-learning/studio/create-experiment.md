---
title: "Uma experimentação simples no Machine Learning Studio | Microsoft Docs"
description: "Este tutorial de machine learning apresenta-lhe uma experimentação de ciência de dados fácil. Vamos prever o preço de um carro através de um algoritmo de regressão."
keywords: "experimentação, regressão linear, algoritmos de machine learning, tutorial de machine learning, técnicas de modelação preditiva, experiência de ciência de dados"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 4cc8e78e3ce22d70546d8a25da17b56f4b7cc166
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Tutorial de Machine Learning: crie a sua primeira experimentação de ciência de dados no Azure Machine Learning Studio

Se nunca utilizou o **Azure Machine Learning Studio**, este tutorial é para si.

Neste tutorial, vamos aprender a utilizar o Studio pela primeira vez para criar uma experimentação de machine learning. A experimentação vai testar um modelo analítico que prevê o preço de um automóvel com base em diferentes variáveis, como a marca e as especificações técnicas.

> [!NOTE]
> Este tutorial mostra-lhe as noções básicas, como arrastar e largar módulos na experimentação, ligá-los entre si, executar a experimentação e analisar os resultados. Não vamos abordar o tópico geral do machine learning nem selecionar e utilizar os mais de cem algoritmos e módulos de manipulação de dados incorporados e incluídos no Studio.
>
>Se não estiver familiarizado com machine learning, a série de vídeos [Data Science for Beginners (Ciência de Dados para Principiantes)](data-science-for-beginners-the-5-questions-data-science-answers.md) pode ser um ponto de partida. Esta série de vídeos é uma excelente introdução ao machine learning, que utiliza uma linguagem e conceitos do dia a dia.
>
>Se já está familiarizado com machine learning, mas está à procura de informações mais genéricas sobre o Machine Learning Studio, bem como os algoritmos de machine learning nele incluídos, eis algums ótimos recursos:
>
- [O que é o Machine Learning Studio?](what-is-ml-studio.md) - Esta é uma descrição geral detalhada do Studio.
- [Machine learning basics with algorithm examples (Noções básicas de machine learning com exemplos de algoritmos)](basics-infographic-with-algorithm-examples.md) - esta infografia é útil se quiser saber mais sobre os diferentes tipos de algoritmos de machine learning que estão incluídos no Machine Learning Studio.
- [Machine Learning Guide (Guia do Machine Learning)](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - este guia abrange informações semelhantes às da infografia anterior, mas num formato interativo.
- [Machine learning algorithm cheat sheet (Referência rápida aos algoritmos de machine learning)](algorithm-cheat-sheet.md) e [How to choose algorithms for Microsoft Azure Machine Learning (Como escolher os algoritmos para o Microsoft Azure Machine Learning)](algorithm-choice.md) - esta imagem e o artigo associado abordam os algoritmos do Studio em maior detalhe.
- [Machine Learning Studio: Algorithm and Module Help (Machine Learning Studio: Ajuda para Algoritmos e Módulos)](https://msdn.microsoft.com/library/azure/dn905974.aspx) - esta é a referência completa para todos os módulos do Studio, incluindo algoritmos de machine learning.

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Como é que o Machine Learning Studio ajuda?

O Machine Learning Studio facilita a configuração de uma experimentação através de módulos de arrastar e largar pré-programados com técnicas de modelação preditiva.

Através de uma área de trabalho interativa e visual, arrasta e larga ***conjuntos de dados*** e ***módulos*** de análises numa tela interativa. Pode ligá-los para formar uma ***experimentação***, que é executada no Machine Learning Studio.
Os modelos são ***criados***, ***preparados*** e ***classificados e testados***.

Pode repetir o design do modelo, editando a experimentação e executando-a até obter os resultados que pretende. Quando o modelo estiver preparado, pode publicá-lo como ***Serviço Web***, para que outras pessoas possam enviar dados novos para o mesmo e, depois, recebam previsões.

## <a name="open-machine-learning-studio"></a>Abrir o Machine Learning Studio

Para começar a utilizar o Studio, aceda a [https://studio.azureml.net](https://studio.azureml.net). Se já tiver iniciado sessão no Machine Learning Studio anteriormente, clique em **Iniciar Sessão**. Caso contrário, clique em **Inscrever-se aqui** e escolha a opção gratuita ou paga.

![Iniciar sessão no Machine Learning Studio][sign-in-to-studio]
<br/>
***Iniciar sessão no Machine Learning Studio***

## <a name="five-steps-to-create-an-experiment"></a>Cinco passos para criar uma experimentação

Neste tutorial do Machine Learning, vai executar cinco passos básicos para criar uma experimentação no Machine Learning Studio, de modo a criar, preparar e classificar o seu modelo:

- **Criar um modelo**
    - [Passo 1: Obter os dados]
    - [Passo 2: Preparar os dados]
    - [Passo 3: Definir funcionalidades]
- **Preparar o modelo**
    - [Passo 4: Escolher e aplicar um algoritmo de aprendizagem]
- **Classificar e testar o modelo**
    - [Passo 5: Prever novos preços para automóveis]

[Passo 1: Obter os dados]: #step-1-get-data
[Passo 2: Preparar os dados]: #step-2-prepare-the-data
[Passo 3: Definir funcionalidades]: #step-3-define-features
[Passo 4: Escolher e aplicar um algoritmo de aprendizagem]: #step-4-choose-and-apply-a-learning-algorithm
[Passo 5: Prever novos preços para automóveis]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Pode encontrar uma cópia de trabalho da experimentação seguinte na [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Aceda a **[Your first data science experiment - Automobile price prediction (A sua primeira experimentação de ciência de dados - Previsão do preço de automóveis)](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** e clique em **Open in Studio (Abrir no Studio)** para transferir uma cópia da experimentação para a sua área de trabalho do Machine Learning Studio.


## <a name="step-1-get-data"></a>Passo 1: Obter os dados

A primeira coisa de que precisa para fazer o machine learning são os dados.
Pode utilizar vários conjuntos de dados de exemplo incluídos no Machine Learning Studio ou pode importar dados de muitas origens. Neste exemplo, vamos utilizar o conjunto de dados de exemplo, **Automobile price data (Raw) (Dados de preços de automóveis (não processados))**, que está incluído na sua área de trabalho.
Este conjunto de dados inclui entradas para vários automóveis individuais, incluindo informações como a marca, o modelo, as especificações técnicas e o preço.

Eis como obter o conjunto de dados na sua experimentação.

1. Crie uma experimentação nova ao clicar em **+NOVA**, na parte inferior da janela Machine Learning Studio, selecione **EXPERIMENTAÇÃO** e, em seguida, selecione **Experimentação em Branco**.

2. É dado um nome predefinido à experimentação, que pode ver na parte superior da tela. Selecione este texto e mude o nome para algo significativo, como, por exemplo, **Previsão de preços de automóveis**. O nome não tem de ser exclusivo.

    ![Mude o nome da experimentação][rename-experiment]

2. À esquerda da tela da experimentação existe uma paleta de conjuntos de dados e módulos. Digite **automóvel** na caixa de pesquisa na parte superior desta paleta para localizar o conjunto de dados denominado **Dados de preços de automóveis (não processados)**. Arraste este conjunto de dados para a tela da experimentação.

    ![Localize o conjunto de dados de automóveis e arraste-o para a tela da experimentação][type-automobile]
    <br/>
    ***Localize o conjunto de dados de automóveis e arraste-o para a tela da experimentação***

Para ver a aparência destes dados, clique na porta exterior da parte inferior do conjunto de dados do automóvel e depois selecione **Visualizar**.

![Clique na porta de saída e selecione "Visualizar"][select-visualize]
<br/>
***Clique na porta de saída e selecione "Visualize" (“Visualizar”)***

> [!TIP]
> Os conjuntos de dados e os módulos têm portas de entrada e de saída, representadas por pequenos círculos. As portas de entrada estão em cima e as de saída estão em baixo.
Para criar um fluxo de dados através da experimentação, ligue uma porta de saída de um módulo a uma porta de entrada de outro.
Pode, em qualquer altura, clicar na porta de saída de um conjunto de dados ou de um módulo para ver o aspeto dos dados nessa fase do fluxo de dados.

Neste conjunto de dados de exemplo, cada instância de um automóvel aparece como uma linha e as variáveis associadas a cada um destes aparecem como colunas. Tendo em conta as variáveis de um automóvel específico, vamos tentar prever o preço na coluna mais à direita (coluna 26, com o nome “preço”).

![Veja os dados dos automóveis na janela de visualização de dados][visualize-auto-data]
<br/>
***Veja os dados dos automóveis na janela de visualização de dados***

Feche a janela de visualização, clicando no "**x**" no canto superior direito.

## <a name="step-2-prepare-the-data"></a>Passo 2: Preparar os dados

Normalmente, um conjunto de dados requer alguns pré-processamentos antes de poder ser analisado. Por exemplo, poderá ter reparado nos valores em falta nas colunas de várias linhas. Estes valores em falta têm de ser apagados para que o modelo possa analisar os dados corretamente. No nosso caso, iremos remover quaisquer linhas que tenham valores em falta. Além disso, a coluna das **perdas normalizadas** tem uma grande proporção de valores em falta, pelo que recomendamos que exclua totalmente essa coluna do modelo.

> [!TIP]
> Apagar os valores em falta a partir dos dados de entrada é um pré-requisito para utilizar a maioria dos módulos.

Primeiro, adicionamos um módulo que remove a coluna **normalized-losses** completamente e, depois, adicionamos outro que remove todas as linhas que tenham dados em falta.

1. Escreva **select columns** na caixa Pesquisa, na parte superior da paleta do módulo, para localizar o módulo [Select Columns in Dataset (Selecionar Colunas do Conjunto de Dados)][select-columns] e arraste-o para a tela de experimentação. Este módulo permite-nos selecionar quais as colunas de dados que pretendemos incluir ou excluir no modelo.

2. Ligue a porta de saída do conjunto de dados **Automobile price data (Raw)** à porta de entrada do módulo [Select Columns in Dataset][select-columns].

    ![Adicione o módulo "Select Columns in Dataset” à tela da experimentação e ligue-o][type-select-columns]
    <br/>
    ***Adicione o módulo "Select Columns in Dataset” à tela da experimentação e ligue-o***

3. Clique no módulo [Select Columns in Dataset][select-columns] e clique em **Launch column selector (Iniciar seletor de colunas)**, no painel **Properties (Propriedades)**.

    - À esquerda, clique em **Com regras**
    - Em **Começar Com**, clique em **Todas as colunas**. Isto instrui o módulo [Select Columns in Dataset][select-columns] a percorrer todas as colunas (exceto as que estamos prestes a excluir).
    - Nas listas pendentes, selecione **Excluir** e os **nomes das colunas** e, em seguida, clique dentro da caixa de texto. É apresentada uma lista de colunas. Selecione **normalized-losses**, que é adicionada à caixa de texto.
    - Clique no botão de marca de verificação (OK) para fechar o seletor de colunas (no canto inferior direito).

    ![Inicie o seletor de colunas e exclua a coluna "normalized-losses"][launch-column-selector]
    <br/>
    ***Inicie o seletor de colunas e exclua a coluna "normalized-losses"***

    Agora, o painel de propriedades de **Select Columns in Datase** indica que o módulo vai percorrer todas as colunas do conjunto de dados, exceto **normalized-losses**.

    ![O painel de propriedades mostra que a coluna "normalized-losses" está excluída][showing-excluded-column]
    <br/>
    ***O painel de propriedades mostra que a coluna "normalized-losses" está excluída***

    > [!TIP]
    Pode adicionar um comentário a um módulo, fazendo duplo clique no módulo e introduzindo o texto. Isto pode ajudá-lo a ver rapidamente o que o módulo está a fazer na sua experimentação. Neste caso, faça duplo clique no módulo [Select Columns in Dataset (Selecionar Colunas no Conjunto de Dados)][select-columns] e escreva o comentário "Exclude normalized losses” (“Excluir perdas normalizadas").
    >
    >


    ![Faça duplo clique num módulo para adicionar um comentário][add-comment]
    <br/>
    ***Faça duplo clique num módulo para adicionar um comentário***

3. Arraste o módulo [Apagar dados em falta][clean-missing-data] para a tela de experimentação e conecte-o ao módulo [Selecionar colunas no conjunto de dados][select-columns]. No painel **Properties**, selecione **Remove entire row (Remover linha inteira)**, em **Cleaning mode (Modo de limpeza)**. Isto instrui [Clean Missing Data (Limpar Dados em Falta)][clean-missing-data] para limpar os dados ao remover as linhas que tenham valores em falta. Clique duas vezes no módulo e escreva o comentário "Remover linhas de valor em falta".

    ![Defina o modo de limpeza como “Remove entire row” no módulo “Clean Missing Data”][set-remove-entire-row]
    <br/>
    ***Defina o modo de limpeza como “Remove entire row” no módulo “Clean Missing Data”***

4. Execute a experimentação clicando em **EXECUTAR** na parte inferior da página.

    Quando a execução da experimentação estiver concluída, todos os módulos têm uma marca de verificação a verde para indicar que foram concluídos com êxito. Repare também no estado **Execução terminada** no canto superior direito.

![Depois de a executar, a experimentação deverá ter este aspeto][early-experiment-run]
<br/>
***Depois de a executar, a experimentação deverá ter este aspeto***

> [!TIP]
> Porque é que executámos a experimentação agora? Ao executar a experimentação, as definições das colunas dos nossos dados passam do conjunto de dados para o módulo [Select Columns in Dataset][select-columns] e para o módulo [Clean Missing Data][clean-missing-data]. Isto significa que qualquer módulo que liguemos a [Clean Missing Data][clean-missing-data] também terá estas informações.

Tudo o que fizemos na experimentação até este ponto foi limpar os dados. Se pretender ver o conjunto de dados limpo, clique na porta de saída à esquerda do módulo [Clean Missing Data][clean-missing-data] e selecione **Visualize**. Repare que a coluna **perdas normalizadas** já não está mais incluída e não existem valores em falta.

Agora que os dados foram apagados, estamos prontos para especificar quais as funcionalidades que vai utilizar no modelo preditivo.

## <a name="step-3-define-features"></a>Passo 3: Definir funcionalidades

No Machine Learning, as *funcionalidades* são propriedades mensuráveis individuais de algo que lhe interessa. No nosso conjunto de dados, cada linha representa um automóvel e cada coluna é uma funcionalidade desse automóvel.

Encontrar um bom conjunto de funcionalidades para criar um modelo preditivo requer experimentação e conhecimentos sobre o problema que pretende resolver. Algumas funcionalidades são melhores para prever num destino do que outras. Além disso, algumas funcionalidades têm uma correlação forte com outras funcionalidades e podem ser removidas. Por exemplo, city-mpg e highway-mpg estão intimamente relacionados, pelo que podemos manter um e remover o outro sem afetar a predição significativamente.

Vamos criar um modelo que utiliza um subconjunto das funcionalidades no nosso conjunto de dados. Pode regressar mais tarde e selecionar funcionalidades diferentes, executar novamente a experimentação e ver se consegue obter melhores resultados. Contudo, para começar, vamos experimentar as seguintes funcionalidades:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Arraste outro módulo [Select Columns in Dataset][select-columns] para a tela da experimentação. Ligue a porta de saída à esquerda do módulo [Clean Missing Data][clean-missing-data] à porta de entrada do módulo [Select Columns in Dataset][select-columns].

    ![Ligue o módulo "Select Columns in Dataset" ao módulo "Clean Missing Data"][connect-clean-to-select]
    <br/>
    ***Ligue o módulo "Select Columns in Dataset" ao módulo "Clean Missing Data"***

2. Clique duas vezes no módulo e escreva "Selecionar as funcionalidades para predição".

2. Clique no painel **Iniciar seletor de colunas** no painel **Propriedades**.

3. Clique em **Com regras**.

4. Em **Begin With (Começar Em)**, clique em **No columns (Nenhuma coluna)**. Na linha do filtro, selecione **Include (Incluir)** e **column names (nomes das colunas)** e selecione a lista de nomes de colunas na caixa de texto. Isto instrui o módulo a não passar por nenhuma coluna (características), exceto por aquelas que especificámos.

5. Clique no botão de marca de verificação (OK).

    ![Selecione as colunas (características) a incluir na predição][select-columns-to-include]
    <br/>
    ***Selecione as colunas (características) a incluir na predição***

Isto resulta num conjunto de dados filtrados que contêm apenas as características que queremos passar para o algoritmo de aprendizagem que vamos utilizar no próximo passo. Mais tarde, pode voltar e tentar novamente com uma seleção de funcionalidades diferente.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Passo 4: Escolher e aplicar um algoritmo de aprendizagem

Agora que os dados estão prontos, construir um modelo preditivo consiste em formar e testar. Utilizaremos os nossos dados para preparar o modelo e, em seguida, vamos testá-lo para ver com que exatidão consegue prever os preços.
<!-- For now, don't worry about *why* we need to train and then test a model.-->

*Classficação* e *regrssão* são dois tipos de algoritmos de machine learning supervisionados. A classificação prevê uma resposta a partir de um conjunto definido de categorias, tais como uma cor (vermelho, azul ou verde). A regressão é utilizada para prever um número.

Uma vez que queremos prever o preço, que é um número, vamos utilizar um algoritmo de regressão. Neste exemplo, vamos utilizar um modelo de *regressão linear* simples.

> [!TIP]
> Se quiser saber mais sobre os diferentes tipos de algoritmos de machine learning e de quando os utilizar, pode ser útil ver o primeiro vídeo da série Data Science for Beginners (Ciência de Dados para Principiantes), [The five questions data science answers (As cinco perguntas às quais a ciência de dados responde)](data-science-for-beginners-the-5-questions-data-science-answers.md). Também pode ser útil ver a infografia [Machine learning basics with algorithm examples](basics-infographic-with-algorithm-examples.md) ou [Machine learning algorithm cheat sheet](algorithm-cheat-sheet.md).

Para preparar o modelo, damos-lhe um conjunto de dados que incluem o preço. O modelo analisa os dados e procura correlações entre as características e o preço de um automóvel. Depois, testamos o modelo. Damos-lhe um conjunto de características de automóveis com que estamos familiarizados e vemos a exatidão com que o modelo consegue prever o preço sabido.

Vamos utilizar os dados quer para preparar o modelo, quer para testá-lo, dividindo-os em conjuntos de dados de preparação e teste separados.

1. Selecione e arraste o módulo [Split Data (Dividir Dados)][split] para a tela da experimentação e ligue-o ao último módulo [Select Columns in Dataset][select-columns].

2. Clique no módulo [Split Data][split] para selecioná-lo. Localize **Fraction of rows in the first output dataset (Fração de linhas no primeiro conjunto de dados de saída)** (no painel **Properties (Propriedades)**, no lado direito da tela) e defina-a como 0,75. Desta forma, vamos utilizar 75% dos dados para preparar o modelo e reter 25% para fins de teste (pode experimentar outras percentagens mais tarde).

    ![Defina a fração de divisão do módulo "Split Data" como 0,75][set-split-data-percentage]
    <br/>
    ***Defina a fração de divisão do módulo "Split Data" como 0,75***

    > [!TIP]
    > Ao alterar o parâmetro **Seed aleatório**, pode produzir diferentes amostras aleatórias para formação e testar. Este parâmetro controla a propagação do gerador de número pseudo-aleatório.

2. Execute a experimentação. Quando a experimentação é executada, os módulos [Select Columns in Dataset][select-columns] e [Split Data][split] passam as definições das colunas para os módulos que vamos adicionar em seguida.  

3. Para selecionar o algoritmo do Learning, expanda a categoria **Machine Learning** na paleta do módulo para a esquerda da tela e, em seguida, expanda **Inicializar modelo**. Isto apresenta várias categorias de módulos que podem ser utilizadas para inicializar algoritmos do Machine Learning. Nesta experimentação, selecione o módulo [Linear Regression (Regressão Linear)][linear-regression], na categoria **Regression (Regressão)** e arraste-o para a tela da experimentação.
(Para encontrar o módulo, também pode escrever “linear regression” na caixa Pesquisa da paleta.)

4. Localize e arraste o módulo [Modelo de formação][train-model] para a tela de experimentação. Ligue a saída do módulo [Linear Regression][linear-regression] à entrada da esquerda do módulo [Train Model][train-model] e ligue a saída de dados de preparação (porta da esquerda) do módulo [Split Data][split] à entrada da direita do módulo [Train Model][train-model].

    ![Ligue o módulo “Train Module” aos módulos “Linear Regression” e “Split Data”][connect-train-model]
    <br/>
    ***Ligue o módulo “Train Module” aos módulos “Linear Regression” e “Split Data”***

5. Clique no módulo [Train Model][train-model], clique em **Launch column selector**no painel **Properties** e selecione a coluna **price (preço)**. Este é o valor que o nosso modelo irá prever.

    Para selecionar a coluna **price** no seletor de colunas, mova-a da lista **Available columns (Colunas disponíveis)** para a lista **Selected columns (Colunas selecionadas)**.

    ![Selecione a coluna de preços do módulo “Train Model”][select-price-column]
    <br/>
    ***Selecione a coluna de preços do módulo “Train Model”***

6. Execute a experimentação.

Temos agora um modelo de regressão preparado que pode ser utilizado para classificar dados de automóveis novos e fazer predições de preços.

![Depois de ser executada, a experimentação deverá ter este aspeto][second-experiment-run]
<br/>
***Depois de ser executada, a experimentação deverá ter este aspeto***

## <a name="step-5-predict-new-automobile-prices"></a>Passo 5: Prever novos preços para automóveis

Agora que experimentámos o modelo, utilizando 75% dos nossos dados, podemos utilizá-lo para pontuar os outros 25% por cento dos dados para ver quão bem funciona o nosso modelo.

1. Localize e arraste o módulo [Score Model (Classificar Modelo)][score-model] para a tela da experimentação. Ligue a saída do módulo [Train Model][train-model] à porta de entrada da esquerda de [Score Model][score-model]. Ligue a saída de dados de teste (porta da direita) do módulo [Split Data][split] à porta de entrada da direita de [Score Model][score-model].

    ![Ligue o módulo "Score Model" aos módulos "Train Model" e "Split Data"][connect-score-model]
    <br/>
    ***Ligue o módulo "Score Model" aos módulos "Train Model" e "Split Data"***

2. Execute a experimentação e veja a saída do módulo [Score Model][score-model] (clique na porta de saída de [Score Model][score-model] e selecione **Visualize**). O resultado mostra os valores previstos para os preços e os valores conhecidos dos dados do teste.  

    ![Saída do módulo “Score Model”][score-model-output]
    <br/>
    ***Saída do módulo “Score Model”***

3. Por fim, vamos testar a qualidade dos resultados. Selecione e arraste o módulo [Evaluate Model (Avaliar Modelo)][evaluate-model] para a tela da experimentação e ligue a saída do módulo [Score Model][score-model] à entrada da esquerda de [Evaluate Model][evaluate-model].

    > [!TIP]
    > Existem duas portas de entrada no módulo [Evaluate Model][evaluate-model], porque este pode ser utilizado para comparar dois modelos lado a lado. Posteriormente, pode adicionar outro algoritmo à experimentação e utilizar [Evaluate Model][evaluate-model] para ver qual dos dois dá melhores resultados.

4. Execute a experimentação.

Para ver o resultado do módulo [Evaluate Model][evaluate-model], clique na porta de saída e, em seguida, selecione **Visualize**.

![Resultados da avaliação da experimentação][evaluation-results]
<br/>
***Resultados da avaliação da experimentação***

As estatísticas seguintes são apresentadas para o nosso modelo:

- **Média dos erros absolutos** (MAE): A média dos erros absolutos (um *erro* é a diferença entre o valor previsto e o valor real).
- **Raiz quadrada da média dos erros** (RMSE): A raiz quadrada da média dos erros ao quadrado das predições efetuadas no conjunto de dados de teste.
- **Erro relativo absoluto**: A média dos erros absolutos relativos à diferença absoluta entre os valores reais e a média de todos os valores reais.
- **Erro ao quadrado absoluto**: A média dos erros ao quadrado relativos à diferença ao quadrado entre os valores reais e a média de todos os valores reais.
- **Coeficiente de determinação**: Também conhecido como o **valor de R ao quadrado**, esta é uma métrica de estatística que indica o quão bem um modelo é adequado para os dados.

Em cada uma das estatísticas de erros, quanto mais pequeno, melhor. Um valor mais pequeno indica que as predições mais detalhadas correspondem aos valores reais. No **Coeficiente de determinação**, quanto mais próximo for um valor de outro (1.0), melhores serão as predições.

## <a name="final-experiment"></a>Experimentação final

A experimentação final deve ter este aspeto:

![A experimentação final][complete-linear-regression-experiment]
<br/>
***A experimentação final***

## <a name="next-steps"></a>Passos seguintes

Agora que concluiu o primeiro tutorial de machine learning e que a sua experimentação está configurada, pode continuar a melhorar o modelo e, depois, implementá-lo como um serviço Web preditivo.

- **Repetir, para tentar melhorar o modelo** - por exemplo, pode alterar as características utilizadas na predição. Em alternativa, pode modificar as propriedades do algoritmo [Linear Regression][linear-regression] ou tentar um algoritmo totalmente diferente. Pode, inclusivamente adicionar, de uma só vez, vários algoritmos de machine learning à sua experimentação e comparar dois deles com o módulo [Evaluate Model][evaluate-model].
Para obter um exemplo de como comparar vários modelos numa experimentação individual, veja [Compare Regressors (Comparar Regressores)](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5), na [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > Para copiar uma repetição da experimentação, utilize o botão **SAVE AS (GUARDAR COMO)**, na parte inferior da página. Pode ver todas as iterações da sua experimentação, clicando em **VER HISTÓRICO DE EXECUÇÕES** na parte inferior da página. Para obter mais detalhes, veja [Manage experiment iterations in Azure Machine Learning Studio (Gerir iterações de experimentações no Azure Machine Learning Studio)][runhistory].

[runhistory]: manage-experiment-iterations.md

- **Implementar o modelo como um serviço Web preditivo** - quando estiver satisfeito com o seu modelo, pode implementá-lo como um serviço Web e utilizá-lo para prever preços de automóveis com dados novos. Para obter mais detalhes, veja [Deploy an Azure Machine Learning web service (Implementar um serviço Web do Azure Machine Learning)][publish].

[publish]: publish-a-machine-learning-web-service.md

Quer saber mais? Para obter instruções mais extensas e detalhadas sobre o processo de criação, preparação, classificação e implementação de um modelo, veja [Desenvolver uma solução preditiva com o Azure Machine Learning][walkthrough].

[walkthrough]: walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/create-experiment/rename-experiment.png
[visualize-auto-data]:./media/create-experiment/visualize-auto-data.png
[select-visualize]: ./media/create-experiment/select-visualize.png
[showing-excluded-column]:./media/create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/create-experiment/second-experiment-run.png
[connect-score-model]:./media/create-experiment/connect-score-model.png
[evaluation-results]:./media/create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/create-experiment/type-automobile.png
[type-select-columns]:./media/create-experiment/type-select-columns.png
[launch-column-selector]:./media/create-experiment/launch-column-selector.png
[add-comment]:./media/create-experiment/add-comment.png
[connect-clean-to-select]:./media/create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[connect-train-model]:./media/create-experiment/connect-train-model.png
[select-price-column]:./media/create-experiment/select-price-column.png

[score-model-output]:./media/create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
