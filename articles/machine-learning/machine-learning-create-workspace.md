---
title: "aaaCreate uma área de trabalho do Machine Learning | Microsoft Docs"
description: "Como toocreate uma área de trabalho para o Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="6009a-103">Criar e partilhar uma área de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6009a-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="6009a-104">Este menu contém ligações tootopics que descrevem como tooset segurança Olá vários ambientes de ciência de dados utilizadas por Olá processo de análise da Cortana (CAPS).</span><span class="sxs-lookup"><span data-stu-id="6009a-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="6009a-105">toouse Azure Machine Learning Studio, terá de toohave uma área de trabalho do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6009a-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="6009a-106">Esta área de trabalho contém as ferramentas de Olá terá toocreate, gerir e publicar experimentações.</span><span class="sxs-lookup"><span data-stu-id="6009a-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="6009a-107">toocreate uma área de trabalho</span><span class="sxs-lookup"><span data-stu-id="6009a-107">toocreate a workspace</span></span>
1. <span data-ttu-id="6009a-108">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6009a-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="6009a-109">toosign no e criar uma área de trabalho, terá de toobe um administrador de subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="6009a-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="6009a-110">Clique em **+ nova**</span><span class="sxs-lookup"><span data-stu-id="6009a-110">Click **+New**</span></span>

3. <span data-ttu-id="6009a-111">Selecione **Intelligence + análise**, clique em **área de trabalho do Machine Learning**, em seguida, clique em **criar**</span><span class="sxs-lookup"><span data-stu-id="6009a-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="6009a-112">Introduza as informações da sua área de trabalho</span><span class="sxs-lookup"><span data-stu-id="6009a-112">Enter your workspace information</span></span>

    - <span data-ttu-id="6009a-113">Olá *nome da área de trabalho* poderá estar cópia de segurança too260 carateres, não que termine num espaço.</span><span class="sxs-lookup"><span data-stu-id="6009a-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="6009a-114">o nome de Olá não pode incluir os seguintes carateres:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="6009a-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="6009a-115">Olá *plano de serviço web* escolher (ou crie), juntamente com Olá associado *escalão de preço* selecione, é utilizada se implementar serviços web desta área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6009a-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Criar uma nova área de trabalho](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="6009a-117">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6009a-117">Click **Create**</span></span>

<span data-ttu-id="6009a-118">Assim que a área de trabalho Olá for implementada, pode abri-lo no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="6009a-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="6009a-119">Procurar tooMachine Learning Studio no [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="6009a-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="6009a-120">Selecione a área de trabalho Olá canto superior direito canto.</span><span class="sxs-lookup"><span data-stu-id="6009a-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Selecione a área de trabalho](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="6009a-122">Clique em **as minhas experimentações**.</span><span class="sxs-lookup"><span data-stu-id="6009a-122">Click **my experiments**.</span></span>

    ![Abra experimentações](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="6009a-124">Para obter informações sobre como gerir a sua área de trabalho, consulte [gerir uma área de trabalho do Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6009a-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="6009a-125">Se ocorrer um problema ao criar a sua área de trabalho, consulte [guia de resolução de problemas: criar e ligar-se a área de trabalho de Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6009a-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="6009a-126">Partilha de uma área de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6009a-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="6009a-127">Quando é criada uma área de trabalho do Machine Learning, pode convidar os utilizadores tooyour área de trabalho tooshare acesso tooyour área de trabalho e todos os respetivos experimentações, conjuntos de dados, blocos de notas, etc. Pode adicionar utilizadores de uma das seguintes duas funções:</span><span class="sxs-lookup"><span data-stu-id="6009a-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="6009a-128">**Utilizador** -um utilizador de área de trabalho pode criar, abrir, modificar e eliminar experimentações, conjuntos de dados, etc. na área de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="6009a-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="6009a-129">**Proprietário** - pode convidar um proprietário e remover utilizadores na área de trabalho de Olá, em adição toowhat um utilizador podem fazer.</span><span class="sxs-lookup"><span data-stu-id="6009a-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="6009a-130">conta de administrador de Olá que cria a área de trabalho Olá é automaticamente adicionada toohello área como proprietário da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6009a-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="6009a-131">No entanto, outros administradores ou utilizadores nessa subscrição não são automaticamente concedidos aceder à área de trabalho toohello - terá tooinvite-los explicitamente.</span><span class="sxs-lookup"><span data-stu-id="6009a-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="6009a-132">tooshare uma área de trabalho</span><span class="sxs-lookup"><span data-stu-id="6009a-132">tooshare a workspace</span></span>

1. <span data-ttu-id="6009a-133">A iniciar sessão tooMachine Learning Studio no [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="6009a-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="6009a-134">No painel esquerdo Olá, clique em **definições**</span><span class="sxs-lookup"><span data-stu-id="6009a-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="6009a-135">Clique em Olá **utilizadores** separador</span><span class="sxs-lookup"><span data-stu-id="6009a-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="6009a-136">Clique em **CONVIDAR utilizadores mais** em Olá parte inferior da página Olá</span><span class="sxs-lookup"><span data-stu-id="6009a-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Definições do Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="6009a-138">Introduza um ou mais endereços de e-mail.</span><span class="sxs-lookup"><span data-stu-id="6009a-138">Enter one or more email addresses.</span></span> <span data-ttu-id="6009a-139">os utilizadores de Olá necessitam de uma conta Microsoft válida ou uma conta institucional (a partir do Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6009a-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="6009a-140">Selecione se pretende que os utilizadores de Olá tooadd como proprietário ou utilizador.</span><span class="sxs-lookup"><span data-stu-id="6009a-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="6009a-141">Clique em Olá **OK** botão de marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="6009a-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="6009a-142">Cada utilizador que adiciona irão receber um e-mail com instruções sobre como toosign no toohello partilhados área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6009a-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="6009a-143">Para os utilizadores toobe capaz de toodeploy ou gerir os serviços web nesta área de trabalho, têm de ser um Contribuidor ou administrador no Olá subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="6009a-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



