---
title: "aaaCreate um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Criar um laboratório no Azure DevTest Labs para máquinas virtuais"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="b9fc0-103">Criar um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9fc0-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="b9fc0-104">Um laboratório no Azure DevTest Labs é infraestrutura Olá que abrange a um grupo de recursos, tais como máquinas virtuais (VMs), que lhe permite um melhor gerir esses recursos, especificando os limites e quotas.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="b9fc0-105">Este artigo explica Olá processo de criação de um laboratório utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9fc0-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9fc0-106">Prerequisites</span></span>
<span data-ttu-id="b9fc0-107">toocreate um laboratório, tem de:</span><span class="sxs-lookup"><span data-stu-id="b9fc0-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="b9fc0-108">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-108">An Azure subscription.</span></span> <span data-ttu-id="b9fc0-109">toolearn sobre as opções de compra do Azure, consulte [como toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="b9fc0-110">Tem de ser o proprietário de Olá de laboratório do Olá subscrição toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="b9fc0-111">Passos toocreate um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b9fc0-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="b9fc0-112">Olá, os passos seguintes mostram como toouse Olá toocreate portal do Azure um laboratório no DevTest Labs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="b9fc0-113">Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="b9fc0-114">No menu principal Olá, no lado esquerdo Olá, selecione **mais serviços** (na Olá parte inferior da lista de Olá).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Opção de menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="b9fc0-116">Na lista de serviços disponíveis, Olá **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="b9fc0-117">No Olá **DevTest Labs** painel, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="b9fc0-119">No Olá **criar um DevTest Lab** painel:</span><span class="sxs-lookup"><span data-stu-id="b9fc0-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="b9fc0-120">Introduza um **nome do laboratório** para laboratório Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="b9fc0-121">Selecione Olá **subscrição** tooassociate com laboratório Olá.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="b9fc0-122">Selecione um **localização** no laboratório de Olá que toostore.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="b9fc0-123">Selecione **encerramento automático** toospecify se pretende tooenable - e definir os parâmetros de Olá-Olá automático a ser encerrado de VMs do laboratório Olá todas as.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="b9fc0-124">Olá funcionalidade de encerramento automático é essencialmente uma funcionalidade de custo guardar na qual pode especificar quando pretende Olá VM tooautomatically ser encerrado.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="b9fc0-125">Pode alterar as definições de encerramento automático depois de criar o laboratório de Olá seguindo os passos de Olá descritos no artigo Olá, [gerir todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="b9fc0-126">Selecione **Pin tooDashboard** se pretender que um atalho de Olá laboratório tooappear no dashboard do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="b9fc0-127">Selecione **opções de automatização** modelos do Azure Resource Manager tooget para a automatização de configuração.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="b9fc0-128">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-128">Select **Create**.</span></span> <span data-ttu-id="b9fc0-129">Depois de selecionar **criar**, Olá **DevTest Labs** apresenta do painel.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="b9fc0-130">Pode monitorizar Estado Olá Olá laboratório do processo de criação, observar Olá **notificações** área.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="b9fc0-131">Depois de concluída, atualização Olá página toosee Olá recém-criado laboratório na lista de Olá de laboratórios.</span><span class="sxs-lookup"><span data-stu-id="b9fc0-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Painel Criar um laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="b9fc0-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b9fc0-133">Next steps</span></span>
<span data-ttu-id="b9fc0-134">Assim que tiver criado o seu laboratório, seguem-se algumas tooconsider passos seguinte:</span><span class="sxs-lookup"><span data-stu-id="b9fc0-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="b9fc0-135">[Laboratório do acesso seguro tooa](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="b9fc0-136">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="b9fc0-137">[Criar um modelo de laboratório](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="b9fc0-138">[Criar artefactos personalizados para as suas VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="b9fc0-139">[Adicionar uma VM com o laboratório de tooa artefactos](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="b9fc0-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

