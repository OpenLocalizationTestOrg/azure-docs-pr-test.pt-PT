---
title: aaaCreate um alerta de registo de atividade com um modelo do Resource Manager | Microsoft Docs
description: "Seja notificado quando são criados os recursos do Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="7e96c-103">Criar um alerta de registo de atividade com um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e96c-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="7e96c-104">Este artigo mostra como toouse um [modelo Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertas de registo de atividade tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7e96c-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="7e96c-105">Utilizando os modelos, pode facilmente definir muitos alertas que ativar com base nas condições de eventos de registo de atividade específica como parte do processo de implementação automática.</span><span class="sxs-lookup"><span data-stu-id="7e96c-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="7e96c-106">passos básico Olá são:</span><span class="sxs-lookup"><span data-stu-id="7e96c-106">hello basic steps are:</span></span>

1. <span data-ttu-id="7e96c-107">Crie um modelo como um ficheiro JSON que descreve como o alerta de registo de atividade de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="7e96c-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="7e96c-108">Implementar a modelo Olá utilizando [qualquer método de implementação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="7e96c-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="7e96c-109">Modelo do Resource Manager para um alerta de registo de atividade</span><span class="sxs-lookup"><span data-stu-id="7e96c-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="7e96c-110">toocreate um alerta de registo de atividade, utilizando um modelo do Resource Manager, criar um recurso do tipo de Olá `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="7e96c-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="7e96c-111">Em seguida, tem de preencher todas as propriedades relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7e96c-111">Then you fill in all related properties.</span></span> <span data-ttu-id="7e96c-112">Segue-se um modelo que cria um alerta de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7e96c-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

<span data-ttu-id="7e96c-113">Visite a nossa [Galeria de início rápido do Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para alguns exemplos de modelos de alerta de registo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7e96c-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e96c-114">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e96c-114">Next steps</span></span>
- <span data-ttu-id="7e96c-115">Saiba mais sobre [alertas](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7e96c-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="7e96c-116">Saiba como tooadd [grupos ação utilizando um modelo do Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="7e96c-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="7e96c-117">Saiba como demasiado[criar um toomonitor de alerta de registo de atividade todas as operações de motor de dimensionamento automático na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="7e96c-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="7e96c-118">Saiba como demasiado[criar um toomonitor de alerta de registo de atividade todas as operações de escala-na/escalável de dimensionamento automático falhou na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="7e96c-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
