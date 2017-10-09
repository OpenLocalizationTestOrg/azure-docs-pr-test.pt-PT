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
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="57d57-103">Instruções passo 4: Preparar e avaliar os modelos de Análise Preditiva Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="57d57-104">Este tópico contém quarto passo de Olá instruções Olá, [desenvolver uma solução de Análise Preditiva no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="57d57-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="57d57-105">Criar uma área de trabalho do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="57d57-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="57d57-106">Carregar os dados existentes</span><span class="sxs-lookup"><span data-stu-id="57d57-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="57d57-107">Criar uma nova experimentação</span><span class="sxs-lookup"><span data-stu-id="57d57-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="57d57-108">**Dar formação e avaliar os modelos de Olá**</span><span class="sxs-lookup"><span data-stu-id="57d57-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="57d57-109">Implementar o serviço Web de Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="57d57-110">Aceder ao serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="57d57-111">Uma das vantagens de Olá da utilização do Azure Machine Learning Studio para criar modelos de machine learning é Olá capacidade tootry mais do que um tipo de modelo de um momento a uma único experimentação e comparar os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="57d57-112">Este tipo de experimentação ajuda-o a determinar a melhor solução de Olá para o seu problema.</span><span class="sxs-lookup"><span data-stu-id="57d57-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="57d57-113">Na experimentação de Olá, iremos estiver a desenvolver esta explicação passo a passo, vamos criar dois tipos diferentes de modelos e, em seguida, compare os respetivos toodecide de resultados de classificação que algoritmo queremos toouse na nossa experimentação final.</span><span class="sxs-lookup"><span data-stu-id="57d57-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="57d57-114">Existem vários modelos, pode escolher a partir do.</span><span class="sxs-lookup"><span data-stu-id="57d57-114">There are various models we could choose from.</span></span> <span data-ttu-id="57d57-115">modelos de Olá toosee disponíveis, expanda Olá **Machine Learning** nó na paleta do módulo Olá e, em seguida, expanda **inicializar modelo** e Olá nós que está abaixo.</span><span class="sxs-lookup"><span data-stu-id="57d57-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="57d57-116">Para efeitos Olá esta fase experimental, iremos selecionar Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] (SVM) e Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulos.</span><span class="sxs-lookup"><span data-stu-id="57d57-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="57d57-117">Ajuda tooget decidir o algoritmo do Machine Learning que melhor se adequa aos problema específico Olá que está a tentar toosolve, consulte [como algoritmos toochoose do Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="57d57-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="57d57-118">Formação Olá modelos</span><span class="sxs-lookup"><span data-stu-id="57d57-118">Train hello models</span></span>

<span data-ttu-id="57d57-119">Vamos adicionar ambos os Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo e [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo deste experimentação.</span><span class="sxs-lookup"><span data-stu-id="57d57-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="57d57-120">Árvore de decisões elevada de duas classes</span><span class="sxs-lookup"><span data-stu-id="57d57-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="57d57-121">Em primeiro lugar, vamos configurar modelo de árvore de decisão Olá elevada.</span><span class="sxs-lookup"><span data-stu-id="57d57-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="57d57-122">Determinar Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo na paleta do módulo Olá e arraste-o para a tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="57d57-123">Determinar Olá [preparar modelo] [ train-model] módulo, arraste-o para a tela Olá e, em seguida, ligue resultado Olá Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree]módulo toohello deixado porta de entrada de Olá [preparar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="57d57-124">Olá [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico Olá e [preparar modelo] [ train-model] utiliza dados de formação modelo de Olá tootrain.</span><span class="sxs-lookup"><span data-stu-id="57d57-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="57d57-125">Ligar a saída à esquerda do Olá da esquerda Olá [executar Script do R] [ execute-r-script] porta de Olá de entrada do módulo toohello direito [preparar modelo] [ train-model] módulo (Iremos decidiu no [passo 3](machine-learning-walkthrough-3-create-new-experiment.md) destes instruções toouse Olá dados provenientes de Olá à esquerda do lado do módulo de dividir dados Olá para formação).</span><span class="sxs-lookup"><span data-stu-id="57d57-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="57d57-126">Já não precisamos duas das entradas de Olá e uma das saídas de Olá da Olá [executar Script do R] [ execute-r-script] módulo para esta fase experimental, pelo que iremos pode deixá-los desanexados.</span><span class="sxs-lookup"><span data-stu-id="57d57-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="57d57-127">Esta parte da experimentação Olá agora aspeto semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="57d57-127">This portion of hello experiment now looks something like this:</span></span>  

![Um modelo de preparação][1]

<span data-ttu-id="57d57-129">Agora precisamos tootell Olá [preparar modelo] [ train-model] módulo que pretende é que o valor do Olá modelo toopredict Olá risco de crédito.</span><span class="sxs-lookup"><span data-stu-id="57d57-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="57d57-130">Selecione Olá [preparar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="57d57-131">No Olá **propriedades** painel, clique em **Seletor de coluna**.</span><span class="sxs-lookup"><span data-stu-id="57d57-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="57d57-132">No Olá **Selecione uma coluna** caixa de diálogo, escreva "risco de crédito" no campo de pesquisa de Olá em **colunas disponíveis**, selecione "Risco de crédito" abaixo e clique no botão de seta para a direita Olá ( **>** ) toomove "De crédito risco" demasiado**colunas selecionadas**.</span><span class="sxs-lookup"><span data-stu-id="57d57-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Selecionar coluna de risco de crédito Olá para o módulo de modelo de formação Olá][0]

3. <span data-ttu-id="57d57-134">Clique em Olá **OK** marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="57d57-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="57d57-135">Máquina de Vetores de Suporte de Duas Classes</span><span class="sxs-lookup"><span data-stu-id="57d57-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="57d57-136">Em seguida, iremos configurar modelo SVM Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="57d57-137">Primeiro, um pequeno explicação sobre SVM.</span><span class="sxs-lookup"><span data-stu-id="57d57-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="57d57-138">Árvores de decisões elevada funcionam bem com funcionalidades de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="57d57-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="57d57-139">No entanto, uma vez que o módulo SVM Olá gera um classificador linear, modelo de Olá gera tem Olá melhor teste erro quando todas as funcionalidades numérico têm Olá mesma escala.</span><span class="sxs-lookup"><span data-stu-id="57d57-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="57d57-140">tooconvert numérico todas as funcionalidades toohello mesmo dimensionar, utilizamos uma transformação "Tanh" (com Olá [normalizar dados] [ normalize-data] módulo).</span><span class="sxs-lookup"><span data-stu-id="57d57-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="57d57-141">Isto transforma nosso números em intervalo Olá [0,1].</span><span class="sxs-lookup"><span data-stu-id="57d57-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="57d57-142">módulo SVM Olá converte cadeia funcionalidades toocategorical, em seguida, toobinary 0/1 e das funcionalidades e, pelo que não suportamos necessário toomanually transformar funcionalidades de cadeia.</span><span class="sxs-lookup"><span data-stu-id="57d57-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="57d57-143">Além disso, não queremos tootransform Olá risco de crédito coluna (21) - é numérico, mas não o valor de Olá que está a formação Olá toopredict de modelo, pelo que temos tooleave-lo individualmente.</span><span class="sxs-lookup"><span data-stu-id="57d57-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="57d57-144">tooset segurança modelo SVM Olá Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="57d57-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="57d57-145">Determinar Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo na paleta do módulo Olá e arraste-o para a tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="57d57-146">Contexto Olá [preparar modelo] [ train-model] módulo, selecione **cópia**e, em seguida, faça duplo clique tela Olá e selecione **colar**.</span><span class="sxs-lookup"><span data-stu-id="57d57-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="57d57-147">Olá cópia Olá [preparar modelo] [ train-model] Olá do módulo é mesmo seleção de coluna como Olá original.</span><span class="sxs-lookup"><span data-stu-id="57d57-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="57d57-148">Ligar o resultado Olá Olá [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo toohello deixado porta de entrada de Olá segundo [preparar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="57d57-149">Determinar Olá [normalizar dados] [ normalize-data] módulo e arraste-o para a tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="57d57-150">Ligar a saída à esquerda do Olá da esquerda Olá [executar Script do R] [ execute-r-script] entrada do módulo toohello deste módulo (tenha em atenção que Olá porta de saída de um módulo pode ser ligado toomore do que um outro módulo).</span><span class="sxs-lookup"><span data-stu-id="57d57-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="57d57-151">Ligar Olá deixado porta de saída do Olá [normalizar dados] [ normalize-data] módulo toohello direito de entrada a porta da Olá segundo [preparar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="57d57-152">Esta parte do nosso experimentação deve agora algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="57d57-152">This portion of our experiment should now look something like this:</span></span>  

![Modelo de segundo formação Olá][2]  

<span data-ttu-id="57d57-154">Configurar agora Olá [normalizar dados] [ normalize-data] módulo:</span><span class="sxs-lookup"><span data-stu-id="57d57-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="57d57-155">Clique em tooselect Olá [normalizar dados] [ normalize-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="57d57-156">No Olá **propriedades** painel, selecione **Tanh** para Olá **método de transformação** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="57d57-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="57d57-157">Clique em **Seletor de coluna**, selecione "Colunas" para **começar com**, selecione **incluir** no Olá primeira lista pendente, selecione **tipo da coluna**no Olá segundo pendente e selecione **numérico** na lista pendente de terceiro Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="57d57-158">Esta ação Especifica que todos os Olá colunas numéricas (e apenas numérica) são transformados.</span><span class="sxs-lookup"><span data-stu-id="57d57-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="57d57-159">Clique em Olá toohello sinal de adição (+) à direita desta linha - esta ação cria uma linha com as dropdowns.</span><span class="sxs-lookup"><span data-stu-id="57d57-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="57d57-160">Selecione **excluir** no Olá primeira lista pendente, selecione **os nomes das colunas** no Olá segundo pendente e introduza "Risco de crédito" no campo de texto Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="57d57-161">Esta ação especifica essa coluna do risco de crédito Olá deve ser ignorada (temos toodo Isto porque esta coluna é numérico e por isso, deverá ser transformado se podemos não excluí-lo).</span><span class="sxs-lookup"><span data-stu-id="57d57-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="57d57-162">Clique em Olá **OK** marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="57d57-162">Click hello **OK** check mark.</span></span>  

    ![Selecionar colunas para o módulo de dados normalizar Olá][5]

<span data-ttu-id="57d57-164">Olá [normalizar dados] [ normalize-data] módulo está agora conjunto tooperform uma transformação Tanh em todas as colunas numérico, exceto para a coluna de risco de crédito Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="57d57-165">Pontuar e avaliar os modelos de Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-165">Score and evaluate hello models</span></span>

<span data-ttu-id="57d57-166">Utilizamos Olá testar os dados que foi separados por Olá [dividir dados] [ split] módulo tooscore nosso modelos de formação.</span><span class="sxs-lookup"><span data-stu-id="57d57-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="57d57-167">Vamos, em seguida, pode comparar Olá os resultados da Olá dois modelos toosee que gerados melhores resultados.</span><span class="sxs-lookup"><span data-stu-id="57d57-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="57d57-168">Adicione módulos do modelo de pontuação de Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="57d57-169">Determinar Olá [Pontuar modelo] [ score-model] módulo e arraste-o para a tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="57d57-170">Ligar Olá [preparar modelo] [ train-model] módulo que estabeleceu toohello [árvore de decisões elevada de duas classes] [ two-class-boosted-decision-tree] entrada à esquerda do módulo toohello porta de Olá [Pontuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="57d57-171">Ligar o direito de Olá [executar Script do R] [ execute-r-script] porta de Olá de entrada do módulo (nossos dados de teste) toohello direito [Pontuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Módulo do modelo de pontuação ligado][6]
   
   <span data-ttu-id="57d57-173">Olá [Pontuar modelo] [ score-model] módulo agora pode demorar informações de crédito Olá de Olá testar dados, executados-o utilizando o modelo de Olá, e os riscos de crédito predições de Olá comparar modelo Olá gera com Olá real coluna na Olá dados de teste.</span><span class="sxs-lookup"><span data-stu-id="57d57-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="57d57-174">Copie e cole Olá [Pontuar modelo] [ score-model] módulo toocreate uma segunda cópia.</span><span class="sxs-lookup"><span data-stu-id="57d57-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="57d57-175">Ligar a saída de Olá do modelo SVM hello (ou seja, Olá saída porta de Olá [preparar modelo] [ train-model] módulo que estabeleceu toohello [máquina de Vetor com suporte de duas classes] [ two-class-support-vector-machine] módulo) toohello entrada porta de Olá segundo [Pontuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="57d57-176">Para o modelo SVM Olá, temos de toodo Olá mesmos dados de teste de transformação toohello como foi feito toohello dados de preparação.</span><span class="sxs-lookup"><span data-stu-id="57d57-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="57d57-177">Por isso, copie e cole Olá [normalizar dados] [ normalize-data] módulo toocreate uma segunda cópia e ligue-o direito de toohello [executar Script do R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="57d57-178">Ligar a saída à esquerda do Olá de Olá segundo [normalizar dados] [ normalize-data] módulo toohello direito de entrada a porta da Olá segundo [Pontuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Ambos os módulos de modelo de pontuação ligados][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="57d57-180">Adicionar módulo do modelo de avaliação de Olá</span><span class="sxs-lookup"><span data-stu-id="57d57-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="57d57-181">tooevaluate Olá resultados de classificação dois e compará-los, utilizamos uma [avaliar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="57d57-182">Determinar Olá [avaliar modelo] [ evaluate-model] módulo e arraste-o para a tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="57d57-183">Ligar a porta de saída de Olá do Olá [Pontuar modelo] [ score-model] módulo associado Olá elevada decisão toohello do modelo de árvore à esquerda de entrada a porta da Olá [avaliar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="57d57-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="57d57-184">Ligar Olá outro [Pontuar modelo] [ score-model] porta de entrada do módulo toohello à direita.</span><span class="sxs-lookup"><span data-stu-id="57d57-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Avaliar modelo módulo ligado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="57d57-186">Execute experimentação Olá e Olá resultados da verificação</span><span class="sxs-lookup"><span data-stu-id="57d57-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="57d57-187">toorun Olá experimentação, clique em Olá **executar** no botão abaixo tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="57d57-188">Pode demorar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="57d57-188">It may take a few minutes.</span></span> <span data-ttu-id="57d57-189">Mostra um indicador de girar em cada módulo que está a ser executado e, em seguida, uma marca de verificação verde mostra quando o módulo Olá estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="57d57-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="57d57-190">Quando todos os módulos de Olá têm uma marca de verificação, experimentação Olá concluiu a execução.</span><span class="sxs-lookup"><span data-stu-id="57d57-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="57d57-191">experimentação Olá deve agora algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="57d57-191">hello experiment should now look something like this:</span></span>  

![Avaliar ambos os modelos][3]

<span data-ttu-id="57d57-193">resultados de Olá toocheck, clique em Olá porta de saída de Olá [avaliar modelo] [ evaluate-model] módulo e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="57d57-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="57d57-194">Olá [avaliar modelo] [ evaluate-model] módulo produz um par de curvas e métricas que lhe permitem resultados de Olá toocompare dos dois modelos de classificadas Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="57d57-195">Pode ver os resultados de Olá como curvas Recetor operador característica (ROC), curvas precisão/devolução de chamada ou curvas de comparação de precisão.</span><span class="sxs-lookup"><span data-stu-id="57d57-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="57d57-196">Dados adicionais apresentados incluem uma matriz de confusão, cumulativos valores para a área de Olá em curva de Olá (AUC) e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="57d57-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="57d57-197">Pode alterar o valor de limiar de Olá ao mover Olá o controlo de deslize esquerdo ou direito e ver como que isso afeta o conjunto de Olá de métricas.</span><span class="sxs-lookup"><span data-stu-id="57d57-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="57d57-198">toohello à direita do gráfico de Olá, clique em **classificada dataset** ou **classificada toocompare de conjunto de dados** toohighlight Olá associado curva e toodisplay Olá associados métricas abaixo.</span><span class="sxs-lookup"><span data-stu-id="57d57-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="57d57-199">Legenda de Olá para curvas Olá, "Classificada o conjunto de dados" corresponde toohello deixado porta de entrada de Olá [avaliar modelo] [ evaluate-model] módulo - no nosso caso, este é o modelo de árvore de decisão Olá elevada.</span><span class="sxs-lookup"><span data-stu-id="57d57-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="57d57-200">"Classificada toocompare de conjunto de dados" corresponde a porta de entrada à direita toohello - modelo SVM Olá no nosso caso.</span><span class="sxs-lookup"><span data-stu-id="57d57-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="57d57-201">Quando clica destas etiquetas, curva Olá para esse modelo é realçada e métricas correspondente Olá são apresentadas, conforme mostrado no Olá gráfico a seguir.</span><span class="sxs-lookup"><span data-stu-id="57d57-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![Curvas ROC para modelos][4]

<span data-ttu-id="57d57-203">Ao examinar estes valores, pode decidir o modelo está mais próximo toogiving que Olá resultados que procura.</span><span class="sxs-lookup"><span data-stu-id="57d57-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="57d57-204">Pode voltar atrás e iterar sua experimentação, alterando os valores de parâmetros em modelos diferentes Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="57d57-205">Ciência Olá e art de interpretar estes resultados e otimização de desempenho do modelo de Olá é exteriores Olá âmbito destas instruções.</span><span class="sxs-lookup"><span data-stu-id="57d57-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="57d57-206">Para obter ajuda adicional, pode ler Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="57d57-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="57d57-207">Como tooevaluate modelo desempenho no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="57d57-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="57d57-208">Escolher os algoritmos de parâmetros toooptimize no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="57d57-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="57d57-209">Interpretar os resultados de modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="57d57-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="57d57-210">Sempre que executar a experimentação Olá um registo desse iteração é mantido no histórico de execuções de Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="57d57-211">Pode ver estes iterações e devolver tooany dos mesmos, clicando **ver histórico de EXECUÇÕES** abaixo tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="57d57-212">Também pode clicar em **executar o anterior** no Olá **propriedades** iteração toohello tooreturn de painel imediatamente anterior Olá um tiver aberto.</span><span class="sxs-lookup"><span data-stu-id="57d57-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="57d57-213">Pode efetuar uma cópia de qualquer iteração da sua experimentação, clicando em **guardar como** abaixo tela Olá.</span><span class="sxs-lookup"><span data-stu-id="57d57-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="57d57-214">Utilize a experimentação de Olá **resumo** e **Descrição** propriedades tookeep um registo das quais já tentou no seu iterações de experimentação.</span><span class="sxs-lookup"><span data-stu-id="57d57-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="57d57-215">Para obter mais detalhes, consulte [gerir iterações de experimentação no Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="57d57-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="57d57-216">**Seguinte: [implementar o serviço web de Olá](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="57d57-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
