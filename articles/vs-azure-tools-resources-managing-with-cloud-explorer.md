---
title: aaaManaging Azure recursos com o Explorador de nuvem | Microsoft Docs
description: Saiba como toouse Cloud Explorer toobrowse e gerir recursos do Azure no Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="54ac3-103">Gerir recursos de Olá associados as contas do Azure no Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="54ac3-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="54ac3-104">Explorador de nuvem permite-lhe tooview os recursos do Azure e os grupos de recursos, verifique as respetivas propriedades e efetuar ações de diagnóstico de chave para programadores no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54ac3-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="54ac3-105">Como Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer baseia-se na pilha do Olá do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="54ac3-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="54ac3-106">Por conseguinte, o Cloud Explorer compreende recursos, tais como grupos de recursos do Azure e serviços do Azure, tais como aplicações lógicas e API apps e suporta [controlo de acesso baseado em funções](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="54ac3-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="54ac3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54ac3-107">Prerequisites</span></span>
- <span data-ttu-id="54ac3-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) com Olá **carga de trabalho do Azure** selecionado, ou uma versão anterior do Visual Studio com Olá [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="54ac3-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="54ac3-109">Conta do Microsoft Azure - se não tiver uma conta, pode [inscrever-se numa avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) ou [ativar os benefícios de subscritor do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="54ac3-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="54ac3-110">tooview Cloud Explorer, selecione **vista** > **Cloud Explorer** na barra de menus Olá.</span><span class="sxs-lookup"><span data-stu-id="54ac3-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="54ac3-111">Adicionar uma conta do Azure de tooCloud Explorer</span><span class="sxs-lookup"><span data-stu-id="54ac3-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="54ac3-112">recursos de Olá tooview associados uma conta do Azure, terá de adicionar primeiro Olá conta tooCloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="54ac3-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="54ac3-113">No **Cloud Explorer**, selecione **as definições da conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="54ac3-115">Selecione **Adicionar nova conta**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-115">Select **Add new account**.</span></span> 

    ![Ligação de adicionar a conta do Explorador de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="54ac3-117">Inicie sessão no toohello conta do Azure cujos recursos que pretende toobrowse.</span><span class="sxs-lookup"><span data-stu-id="54ac3-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="54ac3-118">Depois de a sessão tooan conta do Azure, apresentam subscrições Olá associadas com essa conta.</span><span class="sxs-lookup"><span data-stu-id="54ac3-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="54ac3-119">Selecione as caixas de verificação para as subscrições da conta de Olá que pretende toobrowse e, em seguida, selecione de Olá **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Explorador de nuvem: selecione toodisplay de subscrições do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="54ac3-121">Depois de selecionar subscrições Olá cujos recursos que pretende apresentam toobrowse, essas subscrições e recursos no Olá Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="54ac3-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Nuvem recursos Explorer listagem numa conta do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="54ac3-123">Remover uma conta do Azure a partir do Explorador de nuvem</span><span class="sxs-lookup"><span data-stu-id="54ac3-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="54ac3-124">No **Cloud Explorer**, selecione **as definições da conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="54ac3-126">Selecione o seguinte toohello conta que pretende tooremove, **remover**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="54ac3-128">Ver os tipos de recurso ou grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="54ac3-128">View resource types or resource groups</span></span>
<span data-ttu-id="54ac3-129">tooview os recursos do Azure, pode escolher uma **tipos de recursos** ou **grupos de recursos** vista.</span><span class="sxs-lookup"><span data-stu-id="54ac3-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="54ac3-130">No **Cloud Explorer**, selecione Olá pendente de vista de recursos.</span><span class="sxs-lookup"><span data-stu-id="54ac3-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Vista do Explorador de lista pendente lista tooselect Olá pretendido recursos de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="54ac3-132">No menu de contexto de Olá, selecione a vista de Olá pretendido:</span><span class="sxs-lookup"><span data-stu-id="54ac3-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="54ac3-133">**Tipos de recursos** vista - vista comuns Olá numa Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), mostra os recursos do Azure categorizados pelo respetivo tipo, tais como web apps, contas de armazenamento e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="54ac3-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="54ac3-134">**Grupos de recursos** ver - recursos do Azure categoriza pelo grupo de recursos do Azure de Olá com a qual está associados.</span><span class="sxs-lookup"><span data-stu-id="54ac3-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="54ac3-135">Um grupo de recursos é um pacote de recursos do Azure, normalmente utilizadas por uma aplicação específica.</span><span class="sxs-lookup"><span data-stu-id="54ac3-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="54ac3-136">toolearn mais informações sobre grupos de recursos do Azure, consulte [descrição geral do Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54ac3-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="54ac3-137">Olá imagem seguinte mostra uma comparação de Olá duas vistas de recursos:</span><span class="sxs-lookup"><span data-stu-id="54ac3-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Comparação de vistas de recursos do Explorador da nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="54ac3-139">Ver e navegue recursos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="54ac3-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="54ac3-140">toonavigate tooan recursos do Azure e ver a informação no Cloud Explorer, expanda o grupo de recursos associados ou de tipo do item de Olá e, em seguida, selecione o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ac3-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="54ac3-141">Quando seleciona um recurso, informações aparecem no separadores Olá dois - **ações** e **propriedades** - na Olá parte inferior da Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="54ac3-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="54ac3-142">**Ações** separador - apresenta uma lista de ações de Olá pode efetuar no Cloud Explorer para o recurso de Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="54ac3-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="54ac3-143">Também pode ver estas opções clicando Olá recursos tooview o menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="54ac3-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="54ac3-144">**Propriedades** - separador de propriedades de Olá mostra de recurso de Olá, tal como o grupo de recursos, região e tipo a que está associada.</span><span class="sxs-lookup"><span data-stu-id="54ac3-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="54ac3-145">Olá imagem seguinte mostra uma comparação de exemplo de o que vê em cada separador, para um serviço de aplicações:</span><span class="sxs-lookup"><span data-stu-id="54ac3-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="54ac3-146">Cada recurso tem a ação de Olá **aberto no portal**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="54ac3-147">Ao escolher esta ação, Cloud Explorer apresenta recursos Olá selecionado no Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="54ac3-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="54ac3-148">Olá **aberto no portal** funcionalidade é útil para navegar recursos toodeeply aninhado.</span><span class="sxs-lookup"><span data-stu-id="54ac3-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="54ac3-149">Também podem aparecer com base nos recursos do Azure de Olá ações adicionais e valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="54ac3-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="54ac3-150">Por exemplo, as web apps e logic apps também tem ações Olá **abertos no browser** e **anexar depurador** além demasiado**aberto no portal**.</span><span class="sxs-lookup"><span data-stu-id="54ac3-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="54ac3-151">Editores de tooopen ações aparecem quando seleciona um blob de conta de armazenamento, uma fila ou uma tabela.</span><span class="sxs-lookup"><span data-stu-id="54ac3-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="54ac3-152">As aplicações do Azure têm **URL** e **estado** propriedades, enquanto os recursos de armazenamento ter propriedades de cadeia de ligação e a chave.</span><span class="sxs-lookup"><span data-stu-id="54ac3-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="54ac3-153">Localizar recursos no Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="54ac3-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="54ac3-154">recursos de toolocate com um nome específico nas suas subscrições de conta do Azure, introduza o nome de Olá no Olá **pesquisa** caixa no Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="54ac3-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Localizar recursos na Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="54ac3-156">Como a introduzir carateres no Olá **pesquisa** apresentada a caixa, apenas os recursos que correspondam a esses carateres na árvore de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="54ac3-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
