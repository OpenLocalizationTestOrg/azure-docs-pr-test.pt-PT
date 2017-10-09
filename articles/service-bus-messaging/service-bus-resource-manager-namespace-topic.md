---
title: "aaaCreate Service Bus do Azure espaço de nomes tópico subscrição utilizando o modelo Azure Resource Manager | Microsoft Docs"
description: "Criar um espaço de nomes do Service Bus com o tópico e subscrição utilizando o modelo Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="bff96-103">Criar um espaço de nomes do Service Bus com o tópico e subscrição através de um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bff96-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="bff96-104">Este artigo mostra como toouse um modelo Azure Resource Manager que cria um espaço de nomes do Service Bus e um tópico e uma subscrição dentro desse espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="bff96-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="bff96-105">Ficará a saber como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="bff96-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="bff96-106">Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os requisitos</span><span class="sxs-lookup"><span data-stu-id="bff96-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="bff96-107">Para obter mais informações sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="bff96-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="bff96-108">Para o modelo completo Olá, consulte Olá [espaço de nomes do Service Bus com o tópico e subscrição] [ Service Bus namespace with topic and subscription] modelo.</span><span class="sxs-lookup"><span data-stu-id="bff96-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="bff96-109">Olá seguintes modelos Azure Resource Manager está disponível para transferência e implementação.</span><span class="sxs-lookup"><span data-stu-id="bff96-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="bff96-110">Criar um espaço de nomes do Service Bus</span><span class="sxs-lookup"><span data-stu-id="bff96-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="bff96-111">Criar um espaço de nomes de barramento de serviço com a fila</span><span class="sxs-lookup"><span data-stu-id="bff96-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="bff96-112">Criar um espaço de nomes de barramento de serviço com a regra de autorização e de fila</span><span class="sxs-lookup"><span data-stu-id="bff96-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="bff96-113">Criar um espaço de nomes do Service Bus com o tópico, subscrição e a regra</span><span class="sxs-lookup"><span data-stu-id="bff96-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="bff96-114">toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e procure "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="bff96-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="bff96-115">O que irá implementar?</span><span class="sxs-lookup"><span data-stu-id="bff96-115">What will you deploy?</span></span>

<span data-ttu-id="bff96-116">Com este modelo, irá implementar um espaço de nomes do Service Bus com o tópico e uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="bff96-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="bff96-117">[Tópicos do Service Bus e subscrições](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionar uma forma de um-para-muitos de comunicação, um *publicar/subscrever* padrão.</span><span class="sxs-lookup"><span data-stu-id="bff96-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="bff96-118">toorun Olá automaticamente a implementação, clique em Olá botão os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bff96-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="bff96-119">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bff96-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bff96-120">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="bff96-120">Parameters</span></span>

<span data-ttu-id="bff96-121">Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado.</span><span class="sxs-lookup"><span data-stu-id="bff96-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="bff96-122">modelo de Olá inclui uma secção denominada `Parameters` que contém todos os valores de parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="bff96-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="bff96-123">Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="bff96-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="bff96-124">Não defina parâmetros para valores que sempre permanecerão Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="bff96-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="bff96-125">Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.</span><span class="sxs-lookup"><span data-stu-id="bff96-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="bff96-126">modelo de Olá define Olá seguir os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="bff96-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="bff96-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="bff96-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="bff96-128">nome de Olá do toocreate de espaço de nomes do Service Bus Olá.</span><span class="sxs-lookup"><span data-stu-id="bff96-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="bff96-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="bff96-129">serviceBusTopicName</span></span>
<span data-ttu-id="bff96-130">nome de Olá tópico Olá criado no espaço de nomes de barramento de serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="bff96-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="bff96-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="bff96-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="bff96-132">nome da subscrição Olá criado no espaço de nomes de barramento de serviço de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="bff96-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="bff96-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="bff96-133">serviceBusApiVersion</span></span>
<span data-ttu-id="bff96-134">versão de API do Service Bus de Olá do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bff96-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="bff96-135">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="bff96-135">Resources toodeploy</span></span>
<span data-ttu-id="bff96-136">Cria um espaço de nomes do Service Bus padrão do tipo **mensagens**, com o tópico e uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="bff96-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="bff96-137">Implementação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="bff96-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="bff96-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff96-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="bff96-139">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bff96-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="bff96-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bff96-140">Next steps</span></span>
<span data-ttu-id="bff96-141">Agora que já criou e implementado recursos através do Azure Resource Manager, saiba como toomanage estes recursos visualizando nestes artigos:</span><span class="sxs-lookup"><span data-stu-id="bff96-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="bff96-142">Gerir o barramento de serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff96-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="bff96-143">Gerir recursos do Service Bus com Olá Explorador do Service Bus</span><span class="sxs-lookup"><span data-stu-id="bff96-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
