---
title: "aaaProvision uma Cache de Redis através do Azure Resource Manager | Microsoft Docs"
description: Utilize o Azure Resource Manager modelo toodeploy uma Cache de Redis do Azure.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="6e058-103">Criar uma Cache de Redis com um modelo</span><span class="sxs-lookup"><span data-stu-id="6e058-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="6e058-104">Neste tópico, saiba como toocreate um modelo Azure Resource Manager que implementa do Azure a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="6e058-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="6e058-105">cache de Olá pode ser utilizado com um armazenamento conta tookeep diagnóstico dados existentes.</span><span class="sxs-lookup"><span data-stu-id="6e058-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="6e058-106">Também saber como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="6e058-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="6e058-107">Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="6e058-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="6e058-108">Atualmente, definições de diagnóstico são partilhadas para todas as caches no Olá mesma região para uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="6e058-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="6e058-109">Atualizar uma cache na região de Olá afeta todos os outros caches na região de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e058-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="6e058-110">Para obter mais informações sobre a criação de modelos, consulte [criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6e058-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6e058-111">Para o modelo completo Olá, consulte [modelo de Cache de Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6e058-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="6e058-112">Modelos do Resource Manager para Olá novo [escalão Premium](cache-premium-tier-intro.md) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6e058-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="6e058-113">Criar uma Cache de Redis Premium com clustering</span><span class="sxs-lookup"><span data-stu-id="6e058-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="6e058-114">Criar a Cache de Redis Premium com a persistência de dados</span><span class="sxs-lookup"><span data-stu-id="6e058-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="6e058-115">Criar a Cache de Redis Premium com a VNet e o clustering opcional</span><span class="sxs-lookup"><span data-stu-id="6e058-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="6e058-116">toocheck para modelos de Olá mais recentes, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e procure `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="6e058-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="6e058-117">O que irá implementar</span><span class="sxs-lookup"><span data-stu-id="6e058-117">What you will deploy</span></span>
<span data-ttu-id="6e058-118">Neste modelo, irá implementar uma Cache de Redis do Azure que utiliza uma conta de armazenamento existente para dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6e058-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="6e058-119">toorun Olá automaticamente a implementação, clique em Olá botão os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6e058-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="6e058-120">[![Implementar tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6e058-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="6e058-121">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6e058-121">Parameters</span></span>
<span data-ttu-id="6e058-122">Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado.</span><span class="sxs-lookup"><span data-stu-id="6e058-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="6e058-123">modelo de Olá inclui uma secção denominada parâmetros que contém todos os valores de parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e058-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="6e058-124">Deve definir um parâmetro para esses valores que variam com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="6e058-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="6e058-125">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="6e058-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="6e058-126">Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.</span><span class="sxs-lookup"><span data-stu-id="6e058-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="6e058-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="6e058-127">redisCacheLocation</span></span>
<span data-ttu-id="6e058-128">localização Olá Olá a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="6e058-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="6e058-129">Para melhor desempenho, utilize Olá mesma localização como Olá toobe aplicações utilizada com a cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e058-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="6e058-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="6e058-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="6e058-131">nome de Olá do Olá toouse de conta de armazenamento existente para obter um diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6e058-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="6e058-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="6e058-132">enableNonSslPort</span></span>
<span data-ttu-id="6e058-133">Um valor booleano que indica se tooallow aceder através de portas não SSL.</span><span class="sxs-lookup"><span data-stu-id="6e058-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="6e058-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="6e058-134">diagnosticsStatus</span></span>
<span data-ttu-id="6e058-135">Um valor que indica se o diagnóstico está ativado.</span><span class="sxs-lookup"><span data-stu-id="6e058-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="6e058-136">Utilize ON ou OFF.</span><span class="sxs-lookup"><span data-stu-id="6e058-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="6e058-137">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="6e058-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="6e058-138">Cache de Redis</span><span class="sxs-lookup"><span data-stu-id="6e058-138">Redis Cache</span></span>
<span data-ttu-id="6e058-139">Cria Olá a Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e058-139">Creates hello Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a><span data-ttu-id="6e058-140">Implementação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="6e058-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="6e058-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e058-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="6e058-142">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6e058-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


