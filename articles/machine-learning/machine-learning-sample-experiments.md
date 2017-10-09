---
title: "aaaCopy aprendizagem automática experimentações de exemplo - Azure | Microsoft Docs"
description: "Saiba como aprendizagem de exemplo toouse experimentações toocreate novas experimentações com galeria da Cortana Intelligence e o Microsoft Azure Machine Learning."
keywords: "exemplos machine learning, experimentação de exemplo, machine learning exemplo"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="7b6da-104">Copiar exemplo experimentações toocreate novo do machine learning experimentações</span><span class="sxs-lookup"><span data-stu-id="7b6da-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="7b6da-105">Saiba como toostart com exemplo experimentações do [galeria da Cortana Intelligence](https://gallery.cortanaintelligence.com/) em vez de criar experimentações do machine learning a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="7b6da-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="7b6da-106">Pode utilizar o Olá exemplos toobuild a sua própria solução de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="7b6da-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="7b6da-107">Galeria de Olá tem experimentações de exemplo pela equipa do Microsoft Azure Machine Learning Olá, bem como exemplos partilhados por Olá Comunidade do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7b6da-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="7b6da-108">Também pode colocar questões ou publicar comentários sobre experimentações.</span><span class="sxs-lookup"><span data-stu-id="7b6da-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="7b6da-109">toosee como toouse Olá galeria, veja o vídeo de 3 minutos de Olá [copiar ciência de dados do outras pessoas trabalho toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) da série de Olá [dados de ciência para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="7b6da-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="7b6da-110">Localizar um toocopy experimentação na galeria da Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="7b6da-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="7b6da-111">toosee as experimentações que estão disponível, aceda toohello [galeria](https://gallery.cortanaintelligence.com/) e clique em **experimentações** em Olá parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="7b6da-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="7b6da-112">Localizar Olá experimentações mais recentes ou mais populares</span><span class="sxs-lookup"><span data-stu-id="7b6da-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="7b6da-113">Nesta página, pode ver **recentemente adicionado** experimentações ou, desloque para baixo toolook em **que é popular** ou Olá mais recente **experimentações Microsoft populares**.</span><span class="sxs-lookup"><span data-stu-id="7b6da-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="7b6da-114">Procurar uma experimentação que cumpra os requisitos específicos</span><span class="sxs-lookup"><span data-stu-id="7b6da-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="7b6da-115">toobrowse todas as experimentações:</span><span class="sxs-lookup"><span data-stu-id="7b6da-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="7b6da-116">Clique em **Procurar tudo** em Olá parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="7b6da-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="7b6da-117">No lado esquerdo Olá, sob **refinar por** no Olá **categorias** secção, selecione **experimentação** toosee Olá todas as experimentações na Galeria de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b6da-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="7b6da-118">Pode encontrar experimentações que cumprem os requisitos de duas formas diferentes:</span><span class="sxs-lookup"><span data-stu-id="7b6da-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="7b6da-119">**Selecione os filtros Olá esquerda.**</span><span class="sxs-lookup"><span data-stu-id="7b6da-119">**Select filters on hello left.**</span></span> <span data-ttu-id="7b6da-120">Por exemplo, toobrowse as experimentações que utilizam um algoritmo de deteção de anomalias baseado em PCA: com **experimentação** selecionado em **categorias**, clique em **Mostrar tudo**.</span><span class="sxs-lookup"><span data-stu-id="7b6da-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="7b6da-121">Em seguida, em **Algoritmos Utilizados**, selecione **Deteção de Anomalias Baseada em PCA**.</span><span class="sxs-lookup"><span data-stu-id="7b6da-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="7b6da-122">
     ![Selecionar filtros](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="7b6da-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="7b6da-123">**Utilize a caixa de pesquisa de Olá.**</span><span class="sxs-lookup"><span data-stu-id="7b6da-123">**Use hello search box.**</span></span> <span data-ttu-id="7b6da-124">Por exemplo, toofind experimentações contribuíram pela Microsoft relacionadas com o reconhecimento toodigit que utilizam um algoritmo de máquina de vetor do suporte de classe dois, introduza "reconhecimento de dígitos" na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b6da-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="7b6da-125">Em seguida, selecione Olá filtros **experimentação**, **apenas conteúdo Microsoft**, e **máquina de Vetor com suporte de duas classes**:</span><span class="sxs-lookup"><span data-stu-id="7b6da-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="7b6da-126">
     ![Utilize a caixa de pesquisa de Olá](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="7b6da-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="7b6da-127">Clique em toolearn uma experimentação mais acerca do mesmo.</span><span class="sxs-lookup"><span data-stu-id="7b6da-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="7b6da-128">toorun e/ou modificar a experimentação Olá, clique em **abrir no Studio** na página de Olá experimentação.</span><span class="sxs-lookup"><span data-stu-id="7b6da-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![Experimentação de exemplo](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="7b6da-130">Quando abre uma experimentação no Machine Learning Studio para Olá pela primeira vez, pode Experimente gratuitamente ou comprar uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6da-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="7b6da-131">Saiba mais sobre Olá versão de avaliação gratuita do Machine Learning Studio vs. serviço pago</span><span class="sxs-lookup"><span data-stu-id="7b6da-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="7b6da-132">Criar uma nova experimentação com um exemplo como modelo</span><span class="sxs-lookup"><span data-stu-id="7b6da-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="7b6da-133">Também pode criar uma nova experimentação no Machine Learning Studio através de um exemplo da Galeria como modelo.</span><span class="sxs-lookup"><span data-stu-id="7b6da-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="7b6da-134">Inicie sessão com a sua toohello de credenciais de conta Microsoft [Studio](https://studio.azureml.net)e, em seguida, clique em **novo** toocreate uma experimentação.</span><span class="sxs-lookup"><span data-stu-id="7b6da-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="7b6da-135">Procure o conteúdo de exemplo de Olá e clique em um.</span><span class="sxs-lookup"><span data-stu-id="7b6da-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="7b6da-136">É criada uma nova experimentação na sua área de trabalho de Machine Learning Studio, utilizando a experimentação de exemplo de Olá como um modelo.</span><span class="sxs-lookup"><span data-stu-id="7b6da-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b6da-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b6da-137">Next steps</span></span>
* [<span data-ttu-id="7b6da-138">Importar dados de várias origens</span><span class="sxs-lookup"><span data-stu-id="7b6da-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="7b6da-139">Tutorial de início rápido para o idioma de Olá R no Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b6da-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="7b6da-140">Implementar um serviço Web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b6da-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
