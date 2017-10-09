---
title: recursos de aaaDeploy com a REST API e modelo | Microsoft Docs
description: "Utilize o Azure Resource Manager e a API de REST do Resource Manager toodeploy um tooAzure de recursos. recursos de Olá são definidos num modelo do Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="f93f1-104">Implementar recursos com modelos do Resource Manager e API REST do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f93f1-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f93f1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f93f1-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="f93f1-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f93f1-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="f93f1-107">Portal</span><span class="sxs-lookup"><span data-stu-id="f93f1-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="f93f1-108">API REST</span><span class="sxs-lookup"><span data-stu-id="f93f1-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="f93f1-109">Este artigo explica como toouse Olá API de REST do Resource Manager com o Gestor de recursos modelos toodeploy sua tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="f93f1-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="f93f1-110">Para obter ajuda com a depuração de um erro durante a implementação, consulte:</span><span class="sxs-lookup"><span data-stu-id="f93f1-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="f93f1-111">[Ver as operações de implementação](resource-manager-deployment-operations.md) toolearn sobre como obter as informações que o ajuda a resolver o erro</span><span class="sxs-lookup"><span data-stu-id="f93f1-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="f93f1-112">[Resolver erros comuns ao implementar tooAzure de recursos com o Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn como tooresolve erros de implementação comuns</span><span class="sxs-lookup"><span data-stu-id="f93f1-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="f93f1-113">O modelo pode ser um ficheiro local ou um ficheiro externo que está disponível através de um URI.</span><span class="sxs-lookup"><span data-stu-id="f93f1-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="f93f1-114">Quando o modelo reside numa conta do storage, pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso partilhado durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="f93f1-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="f93f1-115">Implementar com Olá REST API</span><span class="sxs-lookup"><span data-stu-id="f93f1-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="f93f1-116">Definir [cabeçalhos e os parâmetros comuns](https://docs.microsoft.com/rest/api/index), incluindo os tokens de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f93f1-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="f93f1-117">Se não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f93f1-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="f93f1-118">Forneça o ID de subscrição, o nome Olá Olá novo grupo de recursos e localização que precisa para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="f93f1-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="f93f1-119">Para obter mais informações, consulte [criar um grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="f93f1-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="f93f1-120">Validar a sua implementação antes de executá-lo executando Olá [validar uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operação.</span><span class="sxs-lookup"><span data-stu-id="f93f1-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="f93f1-121">Quando a testar a implementação de Olá, fornece os parâmetros exatamente tal como faria ao executar a implementação de Olá (mostrada no passo seguinte Olá).</span><span class="sxs-lookup"><span data-stu-id="f93f1-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="f93f1-122">Crie uma implementação.</span><span class="sxs-lookup"><span data-stu-id="f93f1-122">Create a deployment.</span></span> <span data-ttu-id="f93f1-123">Forneça o ID de subscrição, nome de Olá Olá do grupo de recursos, Olá nome da implementação de Olá e um modelo de tooyour de ligação.</span><span class="sxs-lookup"><span data-stu-id="f93f1-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="f93f1-124">Para obter informações sobre o ficheiro de modelo de Olá, consulte [ficheiro de parâmetros](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="f93f1-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="f93f1-125">Para obter mais informações sobre a REST API de Olá toocreate um grupo de recursos, consulte [criar uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="f93f1-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="f93f1-126">Olá aviso **modo** estiver definido demasiado**Incremental**.</span><span class="sxs-lookup"><span data-stu-id="f93f1-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="f93f1-127">Definir toorun uma implementação completa, **modo** demasiado**concluída**.</span><span class="sxs-lookup"><span data-stu-id="f93f1-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="f93f1-128">Tenha cuidado quando utilizar o modo de conclusão de Olá inadvertidamente pode eliminar os recursos que não estão no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="f93f1-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="f93f1-129">Se pretender que o conteúdo da resposta toolog, conteúdo do pedido ou ambos, incluir **debugSetting** no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="f93f1-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="f93f1-130">Pode configurar o toouse de conta de armazenamento um token de assinatura (SAS) de acesso partilhado.</span><span class="sxs-lookup"><span data-stu-id="f93f1-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="f93f1-131">Para obter mais informações, consulte [delegar o acesso com uma assinatura de acesso partilhado](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="f93f1-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="f93f1-132">Obter o estado de Olá da implementação do modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="f93f1-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="f93f1-133">Para obter mais informações, consulte [obter informações sobre uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="f93f1-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="f93f1-134">Ficheiro de parâmetros</span><span class="sxs-lookup"><span data-stu-id="f93f1-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="f93f1-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f93f1-135">Next steps</span></span>
* <span data-ttu-id="f93f1-136">toolearn sobre como lidar com as operações REST assíncronas, consulte [controlar as operações do Azure assíncronas](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f93f1-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="f93f1-137">Para obter um exemplo de implementação de recursos através da biblioteca de cliente .NET Olá, consulte [implementar recursos através de um modelo e bibliotecas de .NET](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f93f1-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="f93f1-138">toodefine parâmetros no modelo, consulte [criação de modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="f93f1-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="f93f1-139">Para obter orientações sobre como implementar os seus ambientes de toodifferent solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="f93f1-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="f93f1-140">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f93f1-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

