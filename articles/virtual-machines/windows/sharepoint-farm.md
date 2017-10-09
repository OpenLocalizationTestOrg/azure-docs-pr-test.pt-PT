---
title: farms de servidores do SharePoint aaaCreate no Azure | Microsoft Docs
description: "Crie rapidamente um novo farm do SharePoint 2013 ou SharePoint 2016 no Azure utilizando o Olá marketplace portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="74042-103">Criar farms de servidores do SharePoint utilizando Olá marketplace portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74042-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="74042-104">Farms do SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="74042-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="74042-105">Olá Microsoft Azure portal do Marketplace, pode criar rapidamente previamente configuradas farms do SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="74042-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="74042-106">Este modo, pode poupar muito tempo quando precisar de um farm do SharePoint básico ou de elevada disponibilidade para um ambiente de desenvolvimento/teste, ou se estiver a avaliar o SharePoint Server 2013 como uma solução de colaboração para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="74042-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="74042-107">Olá **Farm do SharePoint Server** foi removido um item na Olá Azure Marketplace de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74042-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="74042-108">Foi substituído com Olá **não - HA Farm do SharePoint 2013** e **Farm do SharePoint 2013 HA** itens.</span><span class="sxs-lookup"><span data-stu-id="74042-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="74042-109">farm do SharePoint básico Olá é constituído por três máquinas virtuais nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="74042-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="74042-111">Pode utilizar esta configuração de farm para uma configuração para o desenvolvimento de aplicações do SharePoint simplificada ou avaliação de tempo do primeiro do SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="74042-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="74042-112">toocreate Olá básica () SharePoint farm de três servidores:</span><span class="sxs-lookup"><span data-stu-id="74042-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="74042-113">Clique em [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="74042-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="74042-114">Clique em **implementar**.</span><span class="sxs-lookup"><span data-stu-id="74042-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="74042-115">No Olá **não - HA Farm do SharePoint 2013** painel, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="74042-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="74042-116">Especificar definições nos passos Olá Olá **criar não - HA Farm do SharePoint 2013** painel e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="74042-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="74042-117">farm do SharePoint de elevada disponibilidade de Olá consiste em máquinas virtuais nove nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="74042-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="74042-119">Pode utilizar este farm configuração tootest superiores cliente cargas, a elevada disponibilidade Olá externo de site do SharePoint e grupos de Disponibilidade AlwaysOn do SQL Server para um farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="74042-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="74042-120">Também pode utilizar esta configuração para o desenvolvimento de aplicações do SharePoint num ambiente de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="74042-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="74042-121">farm de SharePoint do toocreate Olá elevada disponibilidade (nove servidor):</span><span class="sxs-lookup"><span data-stu-id="74042-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="74042-122">Clique em [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="74042-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="74042-123">Clique em **implementar**.</span><span class="sxs-lookup"><span data-stu-id="74042-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="74042-124">No Olá **Farm do SharePoint 2013 HA** painel, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="74042-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="74042-125">Especificar definições nos passos Olá sete Olá **criar 2013 HA Farm do SharePoint** painel e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="74042-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="74042-126">Não é possível criar Olá **não - HA Farm do SharePoint 2013** ou **Farm do SharePoint 2013 HA** com uma versão de avaliação gratuita do Azure.</span><span class="sxs-lookup"><span data-stu-id="74042-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="74042-127">Olá portal do Azure cria ambos estes farms numa rede virtual apenas na nuvem com uma presença na web para a Internet.</span><span class="sxs-lookup"><span data-stu-id="74042-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="74042-128">Não há nenhum site para site VPN ou ExpressRoute ligação tooyour back-rede da organização.</span><span class="sxs-lookup"><span data-stu-id="74042-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="74042-129">Quando criar Olá básico ou farms do SharePoint de elevada disponibilidade utilizando Olá portal do Azure, não é possível especificar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="74042-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="74042-130">toowork em torno esta limitação, crie estas farms com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74042-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="74042-131">Para obter mais informações, consulte [farms do SharePoint 2013 criar dev/teste com o Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="74042-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="74042-132">Farms do SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="74042-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="74042-133">Consulte [neste artigo](https://technet.microsoft.com/library/mt723354.aspx) para Olá toobuild instruções de Olá seguinte servidor único SharePoint Server 2016 do farm.</span><span class="sxs-lookup"><span data-stu-id="74042-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="74042-135">Gestão de farms do SharePoint Olá</span><span class="sxs-lookup"><span data-stu-id="74042-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="74042-136">Pode administrar servidores Olá destas farms através de ligações de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="74042-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="74042-137">Para obter mais informações, consulte [iniciar sessão na máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="74042-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="74042-138">Site do SharePoint de Administração Central Olá, pode configurar os meus sites, aplicações do SharePoint e outras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="74042-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="74042-139">Para obter mais informações, consulte [configurar SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="74042-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="74042-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74042-140">Next steps</span></span>
* <span data-ttu-id="74042-141">Detetar adicionais [SharePoint configurações](https://technet.microsoft.com/library/dn635309.aspx) nos serviços de infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="74042-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
