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
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a>Criar um espaço de nomes do Service Bus com o tópico e subscrição através de um modelo Azure Resource Manager

Este artigo mostra como toouse um modelo Azure Resource Manager que cria um espaço de nomes do Service Bus e um tópico e uma subscrição dentro desse espaço de nomes. Ficará a saber como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada. Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os requisitos

Para obter mais informações sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo Olá, consulte Olá [espaço de nomes do Service Bus com o tópico e subscrição] [ Service Bus namespace with topic and subscription] modelo.

> [!NOTE]
> Olá seguintes modelos Azure Resource Manager está disponível para transferência e implementação.
> 
> * [Criar um espaço de nomes do Service Bus](service-bus-resource-manager-namespace.md)
> * [Criar um espaço de nomes de barramento de serviço com a fila](service-bus-resource-manager-namespace-queue.md)
> * [Criar um espaço de nomes de barramento de serviço com a regra de autorização e de fila](service-bus-resource-manager-namespace-auth-rule.md)
> * [Criar um espaço de nomes do Service Bus com o tópico, subscrição e a regra](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e procure "Service Bus".
> 
> 

## <a name="what-will-you-deploy"></a>O que irá implementar?

Com este modelo, irá implementar um espaço de nomes do Service Bus com o tópico e uma subscrição.

[Tópicos do Service Bus e subscrições](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) proporcionar uma forma de um-para-muitos de comunicação, um *publicar/subscrever* padrão.

toorun Olá automaticamente a implementação, clique em Olá botão os seguintes:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)

## <a name="parameters"></a>Parâmetros

Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado. modelo de Olá inclui uma secção denominada `Parameters` que contém todos os valores de parâmetro de Olá. Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar. Não defina parâmetros para valores que sempre permanecerão Olá mesmo. Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.

modelo de Olá define Olá seguir os parâmetros.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nome de Olá do toocreate de espaço de nomes do Service Bus Olá.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
nome de Olá tópico Olá criado no espaço de nomes de barramento de serviço de Olá.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
nome da subscrição Olá criado no espaço de nomes de barramento de serviço de Olá Olá.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versão de API do Service Bus de Olá do modelo de Olá.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>Toodeploy de recursos
Cria um espaço de nomes do Service Bus padrão do tipo **mensagens**, com o tópico e uma subscrição.

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

## <a name="commands-toorun-deployment"></a>Implementação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a>CLI do Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a>Passos seguintes
Agora que já criou e implementado recursos através do Azure Resource Manager, saiba como toomanage estes recursos visualizando nestes artigos:

* [Gerir o barramento de serviço com o PowerShell](service-bus-manage-with-ps.md)
* [Gerir recursos do Service Bus com Olá Explorador do Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
