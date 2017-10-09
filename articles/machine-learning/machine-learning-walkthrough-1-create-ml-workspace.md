---
title: "Passo 1: Criar uma área de trabalho do Machine Learning | Microsoft Docs"
description: "Passo 1 de Olá desenvolver uma solução preditiva explicação passo a passo: Saiba como tooset cópias de segurança nova área de trabalho do Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="64079-103">Passo 1 das Instruções: Criar uma área de trabalho do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="64079-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="64079-104">Este é o primeiro passo de Olá instruções Olá, [desenvolver uma solução de Análise Preditiva no Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="64079-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="64079-105">**Criar uma área de trabalho do Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="64079-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="64079-106">Carregar os dados existentes</span><span class="sxs-lookup"><span data-stu-id="64079-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="64079-107">Criar uma nova experimentação</span><span class="sxs-lookup"><span data-stu-id="64079-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="64079-108">Dar formação e avaliar os modelos de Olá</span><span class="sxs-lookup"><span data-stu-id="64079-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="64079-109">Implementar o serviço Web de Olá</span><span class="sxs-lookup"><span data-stu-id="64079-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="64079-110">Aceder ao serviço Web Olá</span><span class="sxs-lookup"><span data-stu-id="64079-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="64079-111">toouse Machine Learning Studio, terá de toohave uma área de trabalho do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="64079-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="64079-112">Esta área de trabalho contém as ferramentas de Olá terá toocreate, gerir e publicar experimentações.</span><span class="sxs-lookup"><span data-stu-id="64079-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="64079-113">administrador de Olá para a sua subscrição do Azure tem de área de trabalho do toocreate Olá e, em seguida, adicioná-o como um proprietário ou contribuinte.</span><span class="sxs-lookup"><span data-stu-id="64079-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="64079-114">Para obter mais informações, consulte [criar e a partilha de uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="64079-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="64079-115">Depois de criar a sua área de trabalho, abra o Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="64079-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="64079-116">Se tiver mais de uma área de trabalho, pode selecionar área de trabalho Olá na barra de ferramentas de Olá no canto superior direito de Olá da janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="64079-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Selecione a área de trabalho no Studio][2]

> [!TIP]
> <span data-ttu-id="64079-118">Se tiverem sido efetuadas um proprietário da área de trabalho Olá, pode partilhar experimentações Olá que está a trabalhar por outras pessoas inviting toohello área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="64079-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="64079-119">Para fazer isto no Machine Learning Studio no Olá **definições** página.</span><span class="sxs-lookup"><span data-stu-id="64079-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="64079-120">Basta Olá Microsoft conta ou uma conta institucional para cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="64079-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="64079-121">No Olá **definições** página, clique em **utilizadores**, em seguida, clique em **CONVIDAR utilizadores mais** em Olá parte inferior da janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="64079-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="64079-122">**Seguinte: [carregar os dados existentes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="64079-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
