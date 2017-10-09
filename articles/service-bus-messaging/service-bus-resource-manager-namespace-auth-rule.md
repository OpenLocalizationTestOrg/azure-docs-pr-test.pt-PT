---
title: "regra de autorização de Service Bus aaaCreate utilizando o modelo Azure Resource Manager | Microsoft Docs"
description: "Criar uma regra de autorização de barramento de serviço para o espaço de nomes e fila utilizando o modelo Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="5de7a-103">Criar uma regra de autorização de barramento de serviço para o espaço de nomes e fila utilizando um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5de7a-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="5de7a-104">Este artigo mostra como toouse um modelo Azure Resource Manager que cria um [regra de autorização](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para um espaço de nomes de barramento de serviço e fila.</span><span class="sxs-lookup"><span data-stu-id="5de7a-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="5de7a-105">Ficará a saber como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="5de7a-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5de7a-106">Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="5de7a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="5de7a-107">Para obter mais informações sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="5de7a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5de7a-108">Para o modelo completo Olá, consulte Olá [modelo de regra de autorização do Service Bus] [ Service Bus auth rule template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="5de7a-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="5de7a-109">Olá seguintes modelos Azure Resource Manager está disponível para transferência e implementação.</span><span class="sxs-lookup"><span data-stu-id="5de7a-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5de7a-110">Criar um espaço de nomes do Service Bus</span><span class="sxs-lookup"><span data-stu-id="5de7a-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5de7a-111">Criar um espaço de nomes de barramento de serviço com a fila</span><span class="sxs-lookup"><span data-stu-id="5de7a-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="5de7a-112">Criar um espaço de nomes do Service Bus com o tópico e uma subscrição</span><span class="sxs-lookup"><span data-stu-id="5de7a-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="5de7a-113">Criar um espaço de nomes do Service Bus com o tópico, subscrição e a regra</span><span class="sxs-lookup"><span data-stu-id="5de7a-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5de7a-114">toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e procure "Service Bus".</span><span class="sxs-lookup"><span data-stu-id="5de7a-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5de7a-115">O que irá implementar?</span><span class="sxs-lookup"><span data-stu-id="5de7a-115">What will you deploy?</span></span>
<span data-ttu-id="5de7a-116">Com este modelo, irá implementar uma regra de autorização de barramento de serviço para um espaço de nomes e a entidade de mensagens (neste caso, uma fila).</span><span class="sxs-lookup"><span data-stu-id="5de7a-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="5de7a-117">Este modelo utiliza [assinatura de acesso partilhado (SAS)](service-bus-sas.md) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="5de7a-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="5de7a-118">SAS permite que aplicações tooauthenticate tooService Bus utilizando uma chave de acesso configurada no espaço de nomes de Olá, ou Olá mensagens entidade (fila ou um tópico) com os direitos específicos estão associados.</span><span class="sxs-lookup"><span data-stu-id="5de7a-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="5de7a-119">Em seguida, pode utilizar esta chave toogenerate um token SAS que os clientes podem utilizar por sua vez tooauthenticate tooService barramento.</span><span class="sxs-lookup"><span data-stu-id="5de7a-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="5de7a-120">toorun Olá automaticamente a implementação, clique em Olá botão os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5de7a-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5de7a-121">[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5de7a-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5de7a-122">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="5de7a-122">Parameters</span></span>

<span data-ttu-id="5de7a-123">Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado.</span><span class="sxs-lookup"><span data-stu-id="5de7a-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5de7a-124">modelo de Olá inclui uma secção denominada `Parameters` que contém todos os valores de parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="5de7a-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5de7a-125">Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="5de7a-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5de7a-126">Não defina parâmetros para valores que sempre permanecerão Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5de7a-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5de7a-127">Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.</span><span class="sxs-lookup"><span data-stu-id="5de7a-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5de7a-128">modelo de Olá define Olá seguir os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5de7a-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5de7a-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5de7a-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="5de7a-130">nome de Olá do toocreate de espaço de nomes do Service Bus Olá.</span><span class="sxs-lookup"><span data-stu-id="5de7a-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="5de7a-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="5de7a-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="5de7a-132">nome de Olá da regra de autorização de Olá para Olá espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="5de7a-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="5de7a-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="5de7a-133">serviceBusQueueName</span></span>
<span data-ttu-id="5de7a-134">nome da fila de Olá no espaço de nomes de barramento de serviço de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5de7a-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5de7a-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5de7a-135">serviceBusApiVersion</span></span>
<span data-ttu-id="5de7a-136">versão de API do Service Bus de Olá do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5de7a-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="5de7a-137">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="5de7a-137">Resources toodeploy</span></span>
<span data-ttu-id="5de7a-138">Cria um espaço de nomes do Service Bus padrão do tipo **mensagens**e uma regra de autorização de barramento de serviço para o espaço de nomes e a entidade.</span><span class="sxs-lookup"><span data-stu-id="5de7a-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5de7a-139">Implementação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="5de7a-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="5de7a-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5de7a-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5de7a-141">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5de7a-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5de7a-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5de7a-142">Next steps</span></span>
<span data-ttu-id="5de7a-143">Agora que já criou e implementado recursos através do Azure Resource Manager, saiba como toomanage estes recursos visualizando nestes artigos:</span><span class="sxs-lookup"><span data-stu-id="5de7a-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5de7a-144">Gerir o barramento de serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5de7a-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="5de7a-145">Gerir recursos do Service Bus com Olá Explorador do Service Bus</span><span class="sxs-lookup"><span data-stu-id="5de7a-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="5de7a-146">Barramento de serviço de autenticação e autorização</span><span class="sxs-lookup"><span data-stu-id="5de7a-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
