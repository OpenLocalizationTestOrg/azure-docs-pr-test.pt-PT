---
title: aaaDeploy tooAzure Analysis Services utilizando o SSDT | Microsoft Docs
description: Saiba como toodeploy tooan um modelo em tabela do Azure Analysis Services server utilizando o SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="34990-103">Implementar um modelo a partir de SSDT</span><span class="sxs-lookup"><span data-stu-id="34990-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="34990-104">Depois de criar um servidor na sua subscrição do Azure, está pronto toodeploy um tooit de base de dados do modelo de tabela.</span><span class="sxs-lookup"><span data-stu-id="34990-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="34990-105">Pode utilizar o SQL Server Data Tools (SSDT) toobuild e implementar um projeto de modelo em tabela que está a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="34990-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="34990-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="34990-106">Prerequisites</span></span>
<span data-ttu-id="34990-107">tooget iniciada, é necessário:</span><span class="sxs-lookup"><span data-stu-id="34990-107">tooget started, you need:</span></span>

* <span data-ttu-id="34990-108">**Servidor Analysis Services** no Azure.</span><span class="sxs-lookup"><span data-stu-id="34990-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="34990-109">toolearn mais, consulte [criar um servidor de Analysis Services do Azure](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="34990-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="34990-110">**Projeto de modelo em tabela** no SSDT ou um modelo em tabela existente em Olá 1200 ou superior ao nível de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="34990-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="34990-111">Nunca criou um?</span><span class="sxs-lookup"><span data-stu-id="34990-111">Never created one?</span></span> <span data-ttu-id="34990-112">Tente Olá [tutorial de vendas modelação de tabela do Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="34990-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="34990-113">**Gateway no local** -se uma ou mais origens de dados estão no local na rede da sua organização, terá de tooinstall um [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="34990-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="34990-114">gateway de Olá é necessário para o servidor na nuvem de Olá ligar tooyour no local origens tooprocess e atualize dados no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="34990-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="34990-115">Antes de implementar, certifique-se de que pode processar os dados de Olá nas suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="34990-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="34990-116">No SSDT, clique em **Modelo** > **Processar** > **Processar tudo**.</span><span class="sxs-lookup"><span data-stu-id="34990-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="34990-117">Se o processamento falhar, a implementação não é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="34990-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="34990-118">toodeploy um modelo em tabela do SSDT</span><span class="sxs-lookup"><span data-stu-id="34990-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="34990-119">Antes de implementar, terá de nome do servidor tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="34990-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="34990-120">No **portal do Azure** > servidor > **descrição geral** > **nome do servidor**, nome do servidor de Olá de cópia.</span><span class="sxs-lookup"><span data-stu-id="34990-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="34990-122">No SSDT > **Explorador de soluções**, projeto do contexto Olá > **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="34990-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="34990-123">Em seguida, no **implementação** > **servidor** cole o nome do servidor Olá.</span><span class="sxs-lookup"><span data-stu-id="34990-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Colar o nome do servidor na propriedade de implementação do servidor](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="34990-125">Em **Explorador de Soluções**, clique com o botão direito do rato em **Propriedades** e, em seguida, clique em **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="34990-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="34990-126">Poderá ser pedido toosign no tooAzure.</span><span class="sxs-lookup"><span data-stu-id="34990-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Implementar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="34990-128">Estado de implementação é apresentado na janela saída Olá e em implementar.</span><span class="sxs-lookup"><span data-stu-id="34990-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Estado da implementação](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="34990-130">É tudo há tooit!</span><span class="sxs-lookup"><span data-stu-id="34990-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="34990-131">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="34990-131">Troubleshooting</span></span>
<span data-ttu-id="34990-132">Se a implementação falhar quando os metadados de implementação, é provável porque SSDT não foi possível ligar o servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="34990-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="34990-133">Certifique-se de que pode ligar o servidor de tooyour com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="34990-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="34990-134">Em seguida, certifique-se Olá propriedade do servidor de implementação para o projeto de Olá está correto.</span><span class="sxs-lookup"><span data-stu-id="34990-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="34990-135">Se a implementação falhar numa tabela, é provável porque o servidor não foi possível ligar a origem de dados de tooa.</span><span class="sxs-lookup"><span data-stu-id="34990-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="34990-136">Se a origem de dados no local na rede da sua organização, ser tooinstall se um [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="34990-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34990-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34990-137">Next steps</span></span>
<span data-ttu-id="34990-138">Agora que tem o seu servidor do modelo em tabela tooyour implementado, está pronto tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="34990-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="34990-139">Pode [ligar tooit com o SSMS](analysis-services-manage.md) toomanage-lo.</span><span class="sxs-lookup"><span data-stu-id="34990-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="34990-140">E, pode [ligar tooit utilizando uma ferramenta de cliente](analysis-services-connect.md) como Power BI, o Power BI Desktop, ou o Excel e o início a criação de relatórios.</span><span class="sxs-lookup"><span data-stu-id="34990-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

