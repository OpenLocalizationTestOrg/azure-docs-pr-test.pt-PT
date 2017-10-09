---
title: "aplicações geridas do aaaConsume do Azure | Microsoft Docs"
description: "Descreve como um cliente cria um Azure aplicações geridas do ficheiros publicados."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="26c63-103">Consumir uma aplicação gerida interna</span><span class="sxs-lookup"><span data-stu-id="26c63-103">Consume an internal managed application</span></span>

<span data-ttu-id="26c63-104">Pode consumir Azure [geridos aplicações](managed-application-overview.md) que se destinam a ser membros da sua organização.</span><span class="sxs-lookup"><span data-stu-id="26c63-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="26c63-105">Por exemplo, pode selecionar aplicações geridas do departamento de TI garantir a conformidade com as normas organizacionais.</span><span class="sxs-lookup"><span data-stu-id="26c63-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="26c63-106">Estas aplicações geridas estão disponíveis através de Olá catálogo de serviços, Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="26c63-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="26c63-107">Antes de continuar com este artigo, tem de ter uma aplicação gerida disponível no catálogo de serviços de Olá para a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="26c63-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="26c63-108">Se alguém na sua organização não já tiver criado uma aplicação gerida, consulte [publicar uma aplicação gerida para consumo interno](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="26c63-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="26c63-109">Atualmente, pode utilizar a CLI do Azure ou Olá tooconsume do portal do Azure, uma aplicação gerida.</span><span class="sxs-lookup"><span data-stu-id="26c63-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="26c63-110">Criar aplicação Olá gerido utilizando o portal de Olá</span><span class="sxs-lookup"><span data-stu-id="26c63-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="26c63-111">toodeploy uma aplicação gerida através do portal Olá, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="26c63-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="26c63-112">Aceda toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26c63-112">Go toohello Azure portal.</span></span> <span data-ttu-id="26c63-113">Procurar **aplicações geridas do catálogo de serviço**.</span><span class="sxs-lookup"><span data-stu-id="26c63-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Aplicações geridas do catálogo de serviço](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="26c63-115">Selecione Olá geridos aplicação que pretende toocreate da lista de Olá das soluções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="26c63-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="26c63-116">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26c63-116">Select **Create**.</span></span>

   ![Seleção de aplicações geridas](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="26c63-118">Fornece valores para parâmetros de Olá que são necessárias tooprovision Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="26c63-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="26c63-119">Selecione **Central EUA oeste** para a localização.</span><span class="sxs-lookup"><span data-stu-id="26c63-119">Select **West Central US** for location.</span></span> <span data-ttu-id="26c63-120">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="26c63-120">Select **OK**.</span></span>

   ![Parâmetros de aplicações geridas](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="26c63-122">modelo de Olá valida os valores de Olá fornecida.</span><span class="sxs-lookup"><span data-stu-id="26c63-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="26c63-123">Se a validação for bem sucedida, selecione **OK** implementação de Olá toostart.</span><span class="sxs-lookup"><span data-stu-id="26c63-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Validação de aplicações geridas](./media/managed-application-consumption/validation.png)

<span data-ttu-id="26c63-125">Após a conclusão da implementação de Olá, recursos adequados Olá definidos no modelo de Olá aprovisionados no grupo de recursos geridos de Olá fornecida.</span><span class="sxs-lookup"><span data-stu-id="26c63-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="26c63-126">Criar aplicação Olá gerido utilizando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="26c63-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="26c63-127">Existem duas formas toocreate uma aplicação gerida utilizando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="26c63-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="26c63-128">Utilize o comando de Olá para a criação de aplicações geridas.</span><span class="sxs-lookup"><span data-stu-id="26c63-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="26c63-129">Utilize o comando de implementação de modelo normal de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="26c63-130">Utilize o comando de implementação do modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="26c63-130">Use hello template deployment command</span></span>

<span data-ttu-id="26c63-131">Implemente ficheiro applianceMainTemplate.json Olá Olá fornecedor criado.</span><span class="sxs-lookup"><span data-stu-id="26c63-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="26c63-132">Em seguida, crie dois grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="26c63-132">Then create two resource groups.</span></span> <span data-ttu-id="26c63-133">Olá primeiro grupo de recursos é onde hello aplicações geridas recurso é criado: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="26c63-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="26c63-134">grupo de recursos segundo Olá contém todos os recursos de Olá definidos no mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="26c63-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="26c63-135">Este grupo de recursos é gerido pelo Olá ISV.</span><span class="sxs-lookup"><span data-stu-id="26c63-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="26c63-136">Utilize `westcentralus` como localização de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="26c63-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="26c63-137">toodeploy applianceMainTemplate.json no mainResourceGroup, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="26c63-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="26c63-138">Depois de Olá precedente execuções de modelo, este pede-lhe para os valores dos parâmetros de Olá que são definidos no modelo de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="26c63-139">Além disso toohello parâmetros que são necessárias tooprovision recursos num modelo, precisa de dois valores de parâmetro de chave:</span><span class="sxs-lookup"><span data-stu-id="26c63-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="26c63-140">**managedResourceGroupId**: Olá ID Olá recursos grupo contentor Olá recursos definido no applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="26c63-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="26c63-141">ID de Olá tem o formato de Olá `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="26c63-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="26c63-142">No Olá anterior exemplo,-do ID Olá `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="26c63-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="26c63-143">**applianceDefinitionId**: Olá ID Olá geridos recurso de definição de aplicação.</span><span class="sxs-lookup"><span data-stu-id="26c63-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="26c63-144">Este valor é fornecido por Olá ISV.</span><span class="sxs-lookup"><span data-stu-id="26c63-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="26c63-145">publicador de Olá tem de conceder acesso toohello recursos grupo que contém a definição da aplicação Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="26c63-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="26c63-146">recurso de definição de Olá é criado na subscrição do publicador de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="26c63-147">Por conseguinte, um utilizador, grupo de utilizadores ou aplicações no inquilino do cliente Olá tem acesso de leitura toothis recursos.</span><span class="sxs-lookup"><span data-stu-id="26c63-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="26c63-148">Após a conclusão com êxito da implementação de Olá, consulte Olá gerido aplicação é criada no mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="26c63-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="26c63-149">recurso de storageAccount Olá é criado na managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="26c63-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="26c63-150">Olá utilize criar comando</span><span class="sxs-lookup"><span data-stu-id="26c63-150">Use hello create command</span></span>

<span data-ttu-id="26c63-151">Pode utilizar Olá `az managedapp create` comando toocreate uma aplicação gerida Olá geridos definição da aplicação.</span><span class="sxs-lookup"><span data-stu-id="26c63-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="26c63-152">**Id de definição de aplicação**: ID de recurso Olá de Olá gerido criada no Olá precedente passo de definição de aplicação.</span><span class="sxs-lookup"><span data-stu-id="26c63-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="26c63-153">tooobtain este ID, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="26c63-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="26c63-154">Este comando devolve a definição da aplicação Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="26c63-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="26c63-155">É necessário o valor de Olá da propriedade de ID de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="26c63-156">**gerido-rg-id**: nome de Olá Olá recursos grupo contentor Olá recursos definido no applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="26c63-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="26c63-157">Este grupo de recursos é o grupo de recursos geridos de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="26c63-158">É gerida pelo publicador de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-158">It's managed by hello publisher.</span></span> <span data-ttu-id="26c63-159">Se não existir, é criado para si.</span><span class="sxs-lookup"><span data-stu-id="26c63-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="26c63-160">**grupo de recursos**: grupo de recursos de olá onde Olá geridos recurso de aplicação é criado.</span><span class="sxs-lookup"><span data-stu-id="26c63-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="26c63-161">Olá Microsoft.Solutions/appliance recurso se encontra neste grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="26c63-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="26c63-162">**os parâmetros**: Olá parâmetros que são necessários para os recursos de Olá definidos no applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="26c63-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="26c63-163">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="26c63-163">Known issues</span></span>

<span data-ttu-id="26c63-164">Esta versão de pré-visualização inclui Olá os seguintes problemas:</span><span class="sxs-lookup"><span data-stu-id="26c63-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="26c63-165">É apresentado um erro de servidor interno 500 durante a criação de Olá da aplicação Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="26c63-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="26c63-166">Caso se depare com este problema, é provável que toobe intermitente.</span><span class="sxs-lookup"><span data-stu-id="26c63-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="26c63-167">Repita a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-167">Retry hello operation.</span></span>
* <span data-ttu-id="26c63-168">É necessário um novo grupo de recursos para o grupo de recursos geridos de Olá.</span><span class="sxs-lookup"><span data-stu-id="26c63-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="26c63-169">Se utilizar um grupo de recursos existente, a implementação de Olá falhar.</span><span class="sxs-lookup"><span data-stu-id="26c63-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="26c63-170">Olá grupo de recursos contém recursos de Microsoft.Solutions/appliances Olá tem de ser criado no Olá **westcentralus** localização.</span><span class="sxs-lookup"><span data-stu-id="26c63-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26c63-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="26c63-171">Next steps</span></span>

* <span data-ttu-id="26c63-172">Para aplicações de toomanaged uma introdução, consulte [descrição geral de aplicações gerido](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26c63-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="26c63-173">Para obter informações sobre como publicar uma aplicação do catálogo de serviço geridas, consulte [criar e publicar uma aplicação do catálogo de serviço geridas](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="26c63-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="26c63-174">Para obter informações sobre a publicação de aplicações geridas de toohello Azure Marketplace, consulte [Azure geridos aplicações no mercado de Olá](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="26c63-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="26c63-175">Para obter informações sobre a consumir uma aplicação gerida Olá Marketplace, consulte [consuma Azure gerida aplicações no mercado de Olá](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="26c63-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
