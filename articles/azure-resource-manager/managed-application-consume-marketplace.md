---
title: "aaaConsume aplicação gerida do Azure no marketplace | Microsoft Docs"
description: "Describeshow toocreate uma aplicação de gerida do Azure que está disponível através do Olá Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="fa063-103">Consumir Azure geridos aplicações no Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="fa063-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="fa063-104">Tal como explicado Olá [descrição geral de aplicações geridas](managed-application-overview.md) artigo, existem dois cenários Olá final tooend experiência.</span><span class="sxs-lookup"><span data-stu-id="fa063-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="fa063-105">Um é publicador Olá ou o fornecedor que pretende toocreate uma aplicação gerida para utilização pelos clientes.</span><span class="sxs-lookup"><span data-stu-id="fa063-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="fa063-106">Olá segundo é consumidor Olá da aplicação Olá gerido ou o cliente do fim de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa063-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="fa063-107">Este artigo abrange o segundo cenário de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa063-107">This article covers hello second scenario.</span></span> <span data-ttu-id="fa063-108">Descreve como pode implementar uma aplicação gerida Olá Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fa063-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="fa063-109">Criar a partir de Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="fa063-109">Create from hello Marketplace</span></span>

<span data-ttu-id="fa063-110">Implementar uma aplicação gerida Olá Marketplace é semelhante toodeploying qualquer tipo de recursos a partir de Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fa063-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="fa063-111">No portal de Olá, selecione **+ novo** e procure o tipo de Olá de toodeploy de solução.</span><span class="sxs-lookup"><span data-stu-id="fa063-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="fa063-112">Nas opções disponíveis Olá, selecione Olá um que precisa.</span><span class="sxs-lookup"><span data-stu-id="fa063-112">From hello available options, select hello one you need.</span></span>

![soluções de pesquisa](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="fa063-114">Reveja o resumo de Olá da aplicação Olá e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="fa063-114">Review hello summary of hello application, and select **Create**.</span></span>

![criar aplicações geridas](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="fa063-116">Como qualquer outra solução, é apresentada com os valores de tooprovide de campos para.</span><span class="sxs-lookup"><span data-stu-id="fa063-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="fa063-117">Estes campos variam consoante o tipo de Olá da aplicação gerida que cria.</span><span class="sxs-lookup"><span data-stu-id="fa063-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="fa063-118">Ver informações de suporte</span><span class="sxs-lookup"><span data-stu-id="fa063-118">View support information</span></span>

<span data-ttu-id="fa063-119">Após ter implementado a sua aplicação gerida, ver as informações de suporte de Olá para aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fa063-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="fa063-120">No painel de aplicações geridas Olá, as informações de suporte de Olá estão listadas.</span><span class="sxs-lookup"><span data-stu-id="fa063-120">In hello managed application blade, hello support information is listed.</span></span>

![Suporte](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="fa063-122">Permissões do publicador de vista</span><span class="sxs-lookup"><span data-stu-id="fa063-122">View publisher permissions</span></span>

<span data-ttu-id="fa063-123">fornecedor de Olá que gere a sua aplicação é concedido acesso tooyour recursos.</span><span class="sxs-lookup"><span data-stu-id="fa063-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="fa063-124">toosee essas permissões, selecione **autorizações**.</span><span class="sxs-lookup"><span data-stu-id="fa063-124">toosee those permissions, select **Authorizations**.</span></span>

![autorizações](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="fa063-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fa063-126">Next steps</span></span>

* <span data-ttu-id="fa063-127">Para obter informações sobre a publicação de uma aplicação gerida Olá Marketplace, consulte [aplicações geridas do Azure no Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="fa063-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="fa063-128">toopublish geridos aplicações que estão apenas disponíveis toousers na sua organização, consulte [criar e publicar a aplicação gerida do serviço catálogo](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fa063-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="fa063-129">tooconsume geridos aplicações que estão apenas disponíveis toousers na sua organização, consulte [consumir uma aplicação gerida do serviço catálogo](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="fa063-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
