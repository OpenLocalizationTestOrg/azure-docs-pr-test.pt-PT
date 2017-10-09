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
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a>Criar uma regra de autorização de barramento de serviço para o espaço de nomes e fila utilizando um modelo Azure Resource Manager

Este artigo mostra como toouse um modelo Azure Resource Manager que cria um [regra de autorização](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para um espaço de nomes de barramento de serviço e fila. Ficará a saber como toodefine os recursos são implementados e como toodefine parâmetros que são especificados quando a implementação de Olá é executada. Pode utilizar este modelo para as suas próprias implementações ou personalize-toomeet os seus requisitos.

Para obter mais informações sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo Olá, consulte Olá [modelo de regra de autorização do Service Bus] [ Service Bus auth rule template] no GitHub.

> [!NOTE]
> Olá seguintes modelos Azure Resource Manager está disponível para transferência e implementação.
> 
> * [Criar um espaço de nomes do Service Bus](service-bus-resource-manager-namespace.md)
> * [Criar um espaço de nomes de barramento de serviço com a fila](service-bus-resource-manager-namespace-queue.md)
> * [Criar um espaço de nomes do Service Bus com o tópico e uma subscrição](service-bus-resource-manager-namespace-topic.md)
> * [Criar um espaço de nomes do Service Bus com o tópico, subscrição e a regra](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck para modelos de mais recentes Olá, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] Galeria e procure "Service Bus".
> 
> 

## <a name="what-will-you-deploy"></a>O que irá implementar?
Com este modelo, irá implementar uma regra de autorização de barramento de serviço para um espaço de nomes e a entidade de mensagens (neste caso, uma fila).

Este modelo utiliza [assinatura de acesso partilhado (SAS)](service-bus-sas.md) para autenticação. SAS permite que aplicações tooauthenticate tooService Bus utilizando uma chave de acesso configurada no espaço de nomes de Olá, ou Olá mensagens entidade (fila ou um tópico) com os direitos específicos estão associados. Em seguida, pode utilizar esta chave toogenerate um token SAS que os clientes podem utilizar por sua vez tooauthenticate tooService barramento.

toorun Olá automaticamente a implementação, clique em Olá botão os seguintes:

[![Implementar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)

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

### <a name="namespaceauthorizationrulename"></a>namespaceAuthorizationRuleName
nome de Olá da regra de autorização de Olá para Olá espaço de nomes.

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nome da fila de Olá no espaço de nomes de barramento de serviço de Olá Olá.

```json
"serviceBusQueueName": {
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
Cria um espaço de nomes do Service Bus padrão do tipo **mensagens**e uma regra de autorização de barramento de serviço para o espaço de nomes e a entidade.

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

## <a name="commands-toorun-deployment"></a>Implementação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>CLI do Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Passos seguintes
Agora que já criou e implementado recursos através do Azure Resource Manager, saiba como toomanage estes recursos visualizando nestes artigos:

* [Gerir o barramento de serviço com o PowerShell](service-bus-powershell-how-to-provision.md)
* [Gerir recursos do Service Bus com Olá Explorador do Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [Barramento de serviço de autenticação e autorização](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
