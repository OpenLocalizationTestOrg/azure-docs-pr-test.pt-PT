---
title: aaaUse toodeploy portal do Azure recursos do Azure | Microsoft Docs
description: Utilize o portal do Azure e o Azure Resource Manager toodeploy os recursos.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="dfdc0-103">Implementar recursos com modelos do Resource Manager e do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfdc0-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfdc0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfdc0-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="dfdc0-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dfdc0-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="dfdc0-106">Portal</span><span class="sxs-lookup"><span data-stu-id="dfdc0-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="dfdc0-107">API REST</span><span class="sxs-lookup"><span data-stu-id="dfdc0-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="dfdc0-108">Este tópico mostra como toouse Olá [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toodeploy os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="dfdc0-109">toolearn sobre como gerir os recursos, consulte [recursos do Azure de gerir através do portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="dfdc0-110">Atualmente, nem todos os serviço suporta hello portal ou do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="dfdc0-111">Para esses serviços, terá de toouse Olá [portal clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="dfdc0-112">Para o estado de Olá de cada serviço, consulte [gráfico de disponibilidade de portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="dfdc0-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dfdc0-113">Create resource group</span></span>
1. <span data-ttu-id="dfdc0-114">toocreate um grupo de recursos vazio, selecione **novo** > **gestão** > **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![Criar grupo de recursos em branco](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="dfdc0-116">Atribua um nome e localização e, se necessário, selecione uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="dfdc0-117">Precisa de tooprovide uma localização para o grupo de recursos de Olá porque o grupo de recursos de Olá armazena os metadados sobre recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="dfdc0-118">Por motivos de conformidade, poderá ser útil toospecify armazenar esses metadados.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="dfdc0-119">Em geral, recomendamos que especifique uma localização onde a maioria dos seus recursos irá residir.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="dfdc0-120">Utilizar Olá mesma localização pode simplificar o seu modelo.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-120">Using hello same location can simplify your template.</span></span>
   
    ![conjunto de valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="dfdc0-122">Implementar recursos do Marketplace</span><span class="sxs-lookup"><span data-stu-id="dfdc0-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="dfdc0-123">Depois de criar um grupo de recursos, pode implementar recursos tooit de Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="dfdc0-124">Olá Marketplace fornece soluções previamente definidas para cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="dfdc0-125">toostart uma implementação, selecione **novo** e Olá tipo de recurso que gostaria de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="dfdc0-126">Em seguida, procure para versão específica do Olá de recursos de Olá gostaria toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="dfdc0-128">Se não vir solução específica Olá gostaria toodeploy, pode procurar Olá Marketplace-lo.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![marketplace de pesquisa](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="dfdc0-130">Dependendo do tipo de Olá de recursos selecionado, tem uma coleção de propriedades relevantes tooset antes da implementação.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="dfdc0-131">Essas opções não são mostradas aqui, como que variam com base no tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="dfdc0-132">Para todos os tipos, tem de selecionar um grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="dfdc0-133">imagem de Olá seguinte mostra como toocreate uma aplicação web e implementá-la toohello grupo de recursos que criou.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Criar grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="dfdc0-135">Em alternativa, pode decidir toocreate um grupo de recursos quando implementar os recursos.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="dfdc0-136">Selecione **criar nova** e atribua um nome de grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![Criar novo grupo de recursos](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="dfdc0-138">Começa a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-138">Your deployment begins.</span></span> <span data-ttu-id="dfdc0-139">implementação de Olá pode demorar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="dfdc0-140">Quando tiver concluído a implementação de Olá, verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![Vista de notificação](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="dfdc0-142">Depois de implementar os recursos, pode adicionar o grupo de recursos de toohello recursos mais utilizando Olá **adicionar** comando no painel do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![adicionar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="dfdc0-144">Implementar recursos do modelo personalizado</span><span class="sxs-lookup"><span data-stu-id="dfdc0-144">Deploy resources from custom template</span></span>
<span data-ttu-id="dfdc0-145">Se pretender tooexecute uma implementação, mas não utilizar qualquer um dos modelos de Olá no Olá Marketplace, pode criar um modelo personalizado que define a infraestrutura de Olá para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="dfdc0-146">toolearn sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="dfdc0-147">Selecione toodeploy um modelo personalizado através do portal Olá, **novo**e iniciar a pesquisa para **modelo de implementação** até que o pode selecionar opções de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![implementação do modelo de pesquisa](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="dfdc0-149">Selecione **modelo de implementação** a partir dos recursos disponíveis Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![Selecione a implementação do modelo](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="dfdc0-151">Depois de iniciar a implementação do modelo Olá, abra o modelo em branco Olá que está disponível para personalizar.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![Criar modelo](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="dfdc0-153">No editor de Olá, adicione a sintaxe do Olá JSON que define os recursos de Olá pretende toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="dfdc0-154">Selecione **guardar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-154">Select **Save** when done.</span></span> <span data-ttu-id="dfdc0-155">Para obter orientações sobre a sintaxe JSON Olá de escrita, consulte [instruções do modelo do Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![editar modelo](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="dfdc0-157">Em alternativa, pode selecionar um modelo pré-existente de Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="dfdc0-158">Estes modelos são contribuídos por Comunidade Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="dfdc0-159">Estes incluem muitos cenários comuns e alguém adicionou um modelo que é semelhante toowhat que está a tentar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="dfdc0-160">Pode procurar Olá modelos toofind algo que corresponda ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![Selecione o modelo de início rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="dfdc0-162">Pode ver o modelo selecionado Olá num editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="dfdc0-163">Depois de fornecer Olá todos os outros valores, selecione **criar** modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![implementar modelo](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="dfdc0-165">Implementar recursos a partir de um modelo guardado tooyour conta</span><span class="sxs-lookup"><span data-stu-id="dfdc0-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="dfdc0-166">portal Olá permite toosave tooyour um modelo conta do Azure e volte a implementá-lo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="dfdc0-167">Para obter mais informações sobre como trabalhar com estes guardar modelos, [introdução ao modelos privados no portal do Azure de Olá](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="dfdc0-168">Selecione os modelos guardados de toofind **procurar** > **modelos**.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Procurar modelos](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="dfdc0-170">Na lista de Olá dos modelos guardado tooyour conta, selecione Olá um desejar toowork no.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![modelos guardados](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="dfdc0-172">Selecione **implementar** tooredeploy guardar este modelo.</span><span class="sxs-lookup"><span data-stu-id="dfdc0-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![implementar a modelo guardado](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="dfdc0-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dfdc0-174">Next steps</span></span>
* <span data-ttu-id="dfdc0-175">consulte os registos de auditoria tooview, [auditar operações com o Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="dfdc0-176">tootroubleshoot erros de implementação, consulte [ver as operações de implementação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="dfdc0-177">tooretrieve um modelo a partir de uma implementação ou o grupo de recursos, consulte [modelo de exportar o Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="dfdc0-178">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="dfdc0-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

