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
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Implementar recursos com modelos do Resource Manager e API REST do Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI do Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Este artigo explica como toouse Olá API de REST do Resource Manager com o Gestor de recursos modelos toodeploy sua tooAzure de recursos.  

> [!TIP]
> Para obter ajuda com a depuração de um erro durante a implementação, consulte:
> 
> * [Ver as operações de implementação](resource-manager-deployment-operations.md) toolearn sobre como obter as informações que o ajuda a resolver o erro
> * [Resolver erros comuns ao implementar tooAzure de recursos com o Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn como tooresolve erros de implementação comuns
> 
> 

O modelo pode ser um ficheiro local ou um ficheiro externo que está disponível através de um URI. Quando o modelo reside numa conta do storage, pode restringir o modelo de toohello de acesso e fornecer um token de assinatura (SAS) de acesso partilhado durante a implementação.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Implementar com Olá REST API
1. Definir [cabeçalhos e os parâmetros comuns](https://docs.microsoft.com/rest/api/index), incluindo os tokens de autenticação.
2. Se não tiver um grupo de recursos existente, crie um grupo de recursos. Forneça o ID de subscrição, o nome Olá Olá novo grupo de recursos e localização que precisa para a sua solução. Para obter mais informações, consulte [criar um grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Validar a sua implementação antes de executá-lo executando Olá [validar uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operação. Quando a testar a implementação de Olá, fornece os parâmetros exatamente tal como faria ao executar a implementação de Olá (mostrada no passo seguinte Olá).
4. Crie uma implementação. Forneça o ID de subscrição, nome de Olá Olá do grupo de recursos, Olá nome da implementação de Olá e um modelo de tooyour de ligação. Para obter informações sobre o ficheiro de modelo de Olá, consulte [ficheiro de parâmetros](#parameter-file). Para obter mais informações sobre a REST API de Olá toocreate um grupo de recursos, consulte [criar uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Olá aviso **modo** estiver definido demasiado**Incremental**. Definir toorun uma implementação completa, **modo** demasiado**concluída**. Tenha cuidado quando utilizar o modo de conclusão de Olá inadvertidamente pode eliminar os recursos que não estão no seu modelo.
   
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
   
      Se pretender que o conteúdo da resposta toolog, conteúdo do pedido ou ambos, incluir **debugSetting** no pedido de Olá.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Pode configurar o toouse de conta de armazenamento um token de assinatura (SAS) de acesso partilhado. Para obter mais informações, consulte [delegar o acesso com uma assinatura de acesso partilhado](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Obter o estado de Olá da implementação do modelo Olá. Para obter mais informações, consulte [obter informações sobre uma implementação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Ficheiro de parâmetros

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre como lidar com as operações REST assíncronas, consulte [controlar as operações do Azure assíncronas](resource-manager-async-operations.md).
* Para obter um exemplo de implementação de recursos através da biblioteca de cliente .NET Olá, consulte [implementar recursos através de um modelo e bibliotecas de .NET](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toodefine parâmetros no modelo, consulte [criação de modelos](resource-group-authoring-templates.md#parameters).
* Para obter orientações sobre como implementar os seus ambientes de toodifferent solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](solution-dev-test-environments.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

