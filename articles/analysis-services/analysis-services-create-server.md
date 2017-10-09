---
title: aaaCreate um servidor de Analysis Services no Azure | Microsoft Docs
description: "Saiba como toocreate um servidor de Analysis Services instância no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="c3e68-103">Criar um servidor de Analysis Services do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e68-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="c3e68-104">Este artigo explica como criar um recurso de servidor do Analysis Services na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e68-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c3e68-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c3e68-105">Before you begin</span></span>
<span data-ttu-id="c3e68-106">toocomplete este guia de introdução, precisa de:</span><span class="sxs-lookup"><span data-stu-id="c3e68-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="c3e68-107">**Subscrição do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="c3e68-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="c3e68-108">**Azure Active Directory**: sua subscrição tem de ser associada a um inquilino do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3e68-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="c3e68-109">E, terá de toobe com sessão iniciada tooAzure com uma conta no diretório do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3e68-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="c3e68-110">Não são suportadas contas Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c3e68-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="c3e68-111">toolearn mais, consulte [permissões de autenticação e utilizador](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="c3e68-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="c3e68-112">**Grupo de recursos**: Utilize um grupo de recursos já tiver ou [criar um novo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3e68-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c3e68-113">A criação de um servidor poderá resultar num novo serviço sujeito a faturação.</span><span class="sxs-lookup"><span data-stu-id="c3e68-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="c3e68-114">toolearn mais, consulte [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="c3e68-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="c3e68-115">toocreate um servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c3e68-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="c3e68-116">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3e68-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="c3e68-117">Clique em **+ novo** > **dados + análise** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="c3e68-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="c3e68-118">No Olá **Analysis Services** painel, preencha os campos de Olá necessário e, em seguida, prima **criar**.</span><span class="sxs-lookup"><span data-stu-id="c3e68-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Criar servidor do](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="c3e68-120">**Nome do servidor**: escreva um servidor de Olá tooreference exclusivo utilizado.</span><span class="sxs-lookup"><span data-stu-id="c3e68-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="c3e68-121">**Subscrição**: selecione a subscrição de Olá faturas este servidor a.</span><span class="sxs-lookup"><span data-stu-id="c3e68-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="c3e68-122">**Grupo de recursos**: Estes contentores são toohelp concebida gerir uma coleção de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e68-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="c3e68-123">toolearn mais, consulte [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3e68-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="c3e68-124">**Localização**: Olá, anfitriões de localização de centro de dados do Azure este servidor.</span><span class="sxs-lookup"><span data-stu-id="c3e68-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="c3e68-125">Escolha uma localização mais próximo da sua base de utilizadores maior.</span><span class="sxs-lookup"><span data-stu-id="c3e68-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="c3e68-126">**Escalão de preço**: selecione um escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="c3e68-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="c3e68-127">São suportados modelos em tabela segurança too400 GB.</span><span class="sxs-lookup"><span data-stu-id="c3e68-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="c3e68-128">toolearn mais, consulte [preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="c3e68-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="c3e68-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c3e68-129">Click **Create**.</span></span>

<span data-ttu-id="c3e68-130">Criar normalmente tem num minuto; muitas vezes, apenas alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="c3e68-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="c3e68-131">Se tiver selecionado **adicionar tooPortal**, navegue tooyour portal toosee o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="c3e68-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="c3e68-132">Ou, navegue até demasiado**mais serviços** > **Analysis Services** toosee se o servidor está preparado.</span><span class="sxs-lookup"><span data-stu-id="c3e68-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="c3e68-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c3e68-134">Next steps</span></span>
<span data-ttu-id="c3e68-135">Assim que tiver criado o seu servidor, pode [implementar um modelo](analysis-services-deploy.md) tooit utilizando SSDT ou com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="c3e68-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="c3e68-136">Se um modelo de implementar o servidor de tooyour liga origens de dados de tooon local, terá de tooinstall um [gateway de dados no local](analysis-services-gateway.md) num computador na sua rede.</span><span class="sxs-lookup"><span data-stu-id="c3e68-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

