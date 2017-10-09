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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Criar um alerta de registo de atividade com um modelo do Resource Manager
Este artigo mostra como toouse um [modelo Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) alertas de registo de atividade tooconfigure. Utilizando os modelos, pode facilmente definir muitos alertas que ativar com base nas condições de eventos de registo de atividade específica como parte do processo de implementação automática.

passos básico Olá são:

1. Crie um modelo como um ficheiro JSON que descreve como o alerta de registo de atividade de Olá toocreate.

2. Implementar a modelo Olá utilizando [qualquer método de implementação](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Modelo do Resource Manager para um alerta de registo de atividade
toocreate um alerta de registo de atividade, utilizando um modelo do Resource Manager, criar um recurso do tipo de Olá `microsoft.insights/activityLogAlerts`. Em seguida, tem de preencher todas as propriedades relacionadas. Segue-se um modelo que cria um alerta de registo de atividade.

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

Visite a nossa [Galeria de início rápido do Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) para alguns exemplos de modelos de alerta de registo de atividade.

## <a name="next-steps"></a>Passos seguintes
- Saiba mais sobre [alertas](monitoring-overview-alerts.md).
- Saiba como tooadd [grupos ação utilizando um modelo do Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).
- Saiba como demasiado[criar um toomonitor de alerta de registo de atividade todas as operações de motor de dimensionamento automático na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Saiba como demasiado[criar um toomonitor de alerta de registo de atividade todas as operações de escala-na/escalável de dimensionamento automático falhou na sua subscrição](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
