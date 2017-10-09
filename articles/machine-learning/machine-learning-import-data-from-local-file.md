---
title: aaaImport dados de um ficheiro para o Azure Machine Learning Studio | Microsoft Docs
description: "Saiba como tooupload dados de formação do ficheiro do seu disco rígido de tooAzure Machine Learning Studio. Esta ação cria um módulo de conjunto de dados na área de trabalho Olá."
keywords: "Importar dados, o formato de dados, os tipos de dados, as origens de dados, dados de formação"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="674b2-105">Importar dados de formação de um ficheiro no disco rígido no Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="674b2-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="674b2-106">Saiba como tooupload dados de ficheiro do seu disco rígido toouse como dados de formação no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="674b2-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="674b2-107">Ao importar o ficheiro de dados de Olá, tem um módulo de conjunto de dados pronto para ser utilizada em sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="674b2-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="674b2-108">Dados de tooimport passos de um ficheiro local</span><span class="sxs-lookup"><span data-stu-id="674b2-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="674b2-109">tooimport dados a partir de um disco rígido local, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="674b2-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="674b2-110">Clique em **+ novo** em Olá parte inferior da janela de Machine Learning Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="674b2-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="674b2-111">Selecione **DATASET** e **partir do ficheiro LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="674b2-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="674b2-112">No Olá **carregue um novo conjunto de dados** caixa de diálogo, procurar toohello ficheiro pretende tooupload</span><span class="sxs-lookup"><span data-stu-id="674b2-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="674b2-113">Introduza um nome, identifique o tipo de dados de Olá e, opcionalmente, introduza uma descrição.</span><span class="sxs-lookup"><span data-stu-id="674b2-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="674b2-114">Recomenda-se uma descrição - permite-lhe toorecord qualquer caraterísticas sobre dados Olá que pretende que tooremember quando dados Olá Olá futuro.</span><span class="sxs-lookup"><span data-stu-id="674b2-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="674b2-115">caixa de verificação de Olá **esta é a versão nova do Olá de um conjunto de dados existente** permite-lhe tooupdate um conjunto de dados existente com novos dados.</span><span class="sxs-lookup"><span data-stu-id="674b2-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="674b2-116">Clique nesta caixa de verificação e, em seguida, introduza o nome de Olá de um conjunto de dados existente.</span><span class="sxs-lookup"><span data-stu-id="674b2-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Carregue um novo conjunto de dados](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="674b2-118">Durante o carregamento, verá uma mensagem que o ficheiro está a ser carregado.</span><span class="sxs-lookup"><span data-stu-id="674b2-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="674b2-119">Carregar tempo depende do tamanho de Olá dos seus dados e Olá velocidade do seu serviço de toohello de ligação.</span><span class="sxs-lookup"><span data-stu-id="674b2-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="674b2-120">Se souber o ficheiro de Olá irá demorar muito tempo, pode efetuar outras ações no interior do Machine Learning Studio enquanto aguarde.</span><span class="sxs-lookup"><span data-stu-id="674b2-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="674b2-121">No entanto, a fechar o browser Olá provoca toofail de carregamento de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="674b2-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="674b2-122">Módulo de conjunto de dados está pronto a utilizar</span><span class="sxs-lookup"><span data-stu-id="674b2-122">Dataset module is ready for use</span></span>
<span data-ttu-id="674b2-123">Depois dos dados são carregados, é armazenado num módulo conjunto de dados e está disponível tooany experimentação na sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="674b2-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="674b2-124">Quando estiver a editar uma experimentação, pode encontrar Olá conjuntos de dados que criou no Olá **conjuntos de dados os meus** lista em Olá **conjuntos de dados guardado** lista na paleta do módulo Olá.</span><span class="sxs-lookup"><span data-stu-id="674b2-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="674b2-125">Pode arrastar e largar Olá conjunto de dados para a tela de experimentação do Olá quando pretender que o conjunto de dados do toouse Olá para análise adicional e a aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="674b2-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
