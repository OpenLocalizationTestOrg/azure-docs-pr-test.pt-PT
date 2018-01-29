---
title: "Criar experimentações de exemplo de machine learning - Azure | Microsoft Docs"
description: "Saiba como utilizar experimentações de exemplo de machine learning para criar novas experimentações com a Galeria de IA do Azure e com o Azure Machine Learning."
keywords: "exemplos machine learning, experimentação de exemplo, machine learning exemplo, exemplos IA"
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
ms.date: 01/05/2018
ms.author: cgronlun
ms.openlocfilehash: 9ea19f137acb23d3527315aae2624c746e138545
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/05/2018
---
# <a name="create-machine-learning-experiments-from-working-examples-in-azure-ai-gallery"></a>Criar experimentações do machine learning a partir de exemplos de trabalho na Galeria de AI do Azure

Saiba como iniciar experimentações de exemplo a partir da [Galeria de IA do Azure](https://gallery.cortanaintelligence.com/), em vez de criar experimentações de machine learning do zero. Pode utilizar os exemplos para criar a sua própria solução de machine learning.

A galeria apresenta exemplos de experimentações da equipa do Microsoft Azure Machine Learning, bem como exemplos partilhados pela Comunidade do Machine Learning. Também pode colocar questões ou publicar comentários sobre experimentações.

Para saber como utilizar a galeria, veja o vídeo de 3 minutos [Copy other people's work to do data science (Copiar o trabalho de outras pessoas para efetuar ciência de dados)](data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) da série [Data Science for Beginners (Ciência de Dados para Principiantes)](data-science-for-beginners-the-5-questions-data-science-answers.md).

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-azure-ai-gallery"></a>Encontrar uma experimentação para copiar na Galeria de IA do Azure
Para ver as experimentações que estão disponíveis, aceda à [Galeria](https://gallery.cortanaintelligence.com/) e clique em **Experimentações** na parte superior da página.

### <a name="find-the-newest-or-most-popular-experiments"></a>Localizar as experimentações mais recentes ou mais populares
Nesta página, pode ver as experimentações **Recentemente adicionadas** ou deslocar para baixo para ver **O que é popular** ou as **experimentações Microsoft populares** mais recentes.

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a>Procurar uma experimentação que cumpra os requisitos específicos
Para procurar todas as experimentações:

1. Clique em **Procurar tudo** na parte superior da página.
2. No lado esquerdo, em **Refinar por** na secção **Categorias**, selecione **Experimentação** para ver todas as experimentações na Galeria.
3. Pode encontrar experimentações que cumprem os requisitos de duas formas diferentes:
   * **Selecione filtros no lado esquerdo.** Por exemplo, para procurar experimentações que utilizem um algoritmo de deteção de anomalias baseado em PCA: em **Categorias**, clique em **Experimentação**. Em seguida, em **Algoritmos Utilizados**, clique em **Mostrar tudo** e, na caixa de diálogo, escolha **Deteção de Anomalias Baseada em PCA**. Poderá ter de deslocar para baixo para vê-la.<br></br>
     ![Selecionar filtros](./media/sample-experiments/choose-an-algorithm.png)
   * **Utilize a caixa de pesquisa.** Por exemplo, para procurar experimentações que tenham feito parte da Microsoft e estejam relacionadas com o reconhecimento de dígitos que utilizam um algoritmo da máquina de vetor com suporte de classe dois, introduza "reconhecimento de dígitos" na caixa de pesquisa. Em seguida, selecione os filtros **Experimentação**, **Apenas conteúdos da Microsoft** e **Máquina de Vetor com Suporte de Classe Dois**:<br></br>
     ![Utilizar a caixa de pesquisa](./media/sample-experiments/search-for-experiments.png)
4. Clique numa experimentação para saber mais acerca da mesma.
5. Para executar e/ou modificar a experimentação, clique em **Abrir no Studio** na página de experimentação. <br></br>

    ![Experimentação de exemplo](./media/sample-experiments/example-experiment.png)

    > [!NOTE]
    > Quando abre uma experimentação no Machine Learning Studio pela primeira vez, pode experimentar gratuitamente ou comprar uma subscrição do Azure. [Saiba mais sobre a avaliação gratuita do Machine Learning Studio vs. serviço pago](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a>Criar uma nova experimentação com um exemplo como modelo
Também pode criar uma nova experimentação no Machine Learning Studio através de um exemplo da Galeria como modelo.

1. Inicie sessão com as credenciais da sua conta Microsoft no [Studio](https://studio.azureml.net) e, em seguida, clique em **Novo** para criar uma experimentação.
2. Navegue no conteúdo de exemplos e clique num deles.

É criada uma nova experimentação na sua área de trabalho do Machine Learning Studio através da experimentação de exemplo como modelo.

## <a name="next-steps"></a>Passos seguintes
* [Importar dados de várias origens](import-data.md)
* [Tutorial de início rápido para a linguagem R no Machine Learning](r-quickstart.md)
* [Implementar um serviço Web Machine Learning](publish-a-machine-learning-web-service.md)
