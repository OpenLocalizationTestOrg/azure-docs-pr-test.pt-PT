---
title: "aaaAutomatically ativar as definições de diagnóstico com um modelo do Resource Manager | Microsoft Docs"
description: "Saiba como toouse um Gestor de recursos do modelo toocreate definições de diagnóstico que vão permitir toostream o diagnóstico regista tooEvent Hubs ou armazená-las numa conta do storage."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Ativar automaticamente definições de diagnóstico durante a criação de recursos através de um modelo do Resource Manager
Neste artigo mostramos como pode utilizar um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure definições de diagnóstico num recurso quando é criado. Isto permite-lhe iniciar tooautomatically sua tooEvent métricas e registos de diagnóstico Hubs, arquivá-los numa conta de armazenamento ou enviar-lhes tooLog análise quando é criado um recurso de transmissão em fluxo.

método de Olá para ativar os registos de diagnóstico com um modelo do Resource Manager depende do tipo de recurso Olá.

* **Computação não** recursos (por exemplo, grupos de segurança de rede, as Logic Apps, automatização) [definições de diagnóstico descrito neste artigo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Computação** recursos (WAD/LAD baseado) utilizam Olá [ficheiro de configuração de WAD/LAD descrito neste artigo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

Este artigo descreve como os diagnósticos de tooconfigure utilizando um dos métodos.

os passos básicos de Olá são os seguintes:

1. Crie um modelo como um ficheiro JSON que descreve como toocreate Olá recursos e ative os diagnósticos.
2. [Implementar a modelo Olá com qualquer método de implementação](../azure-resource-manager/resource-group-template-deploy.md).

Abaixo que lhe damos um exemplo de modelo de Olá ficheiro JSON tem toogenerate de não computação e de recursos de computação.

## <a name="non-compute-resource-template"></a>Modelo de recursos de computação não
Não-recursos de computação, terá de toodo duas coisas:

1. Adicione o blob de parâmetros de toohello parâmetros para o nome de conta do storage Olá, ID de regra de barramento de serviço e/ou ID da área de trabalho de análise de registos do OMS (ativar o arquivo de registos de diagnóstico numa conta do storage, transmissão em fluxo de registos tooEvent Hubs e/ou envio de registos tooLog análise).
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. Na matriz de recursos de Olá do recurso de Olá para o qual pretende que os registos de diagnóstico tooenable, adicione um recurso do tipo `[resource namespace]/providers/diagnosticSettings`.
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

Olá blob de propriedades para a definição de diagnóstico de Olá segue [formato Olá descrito neste artigo](https://msdn.microsoft.com/library/azure/dn931931.aspx). Adicionar Olá `metrics` propriedade permitirá toothese métricas tooalso envio recursos mesmo produz, fornecido que [recursos Olá suporta métricas de Monitor de Azure](monitoring-supported-metrics.md).

Eis um exemplo completo que cria uma aplicação lógica e ativa a transmissão em fluxo tooEvent Hubs e armazenamento numa conta do storage.

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a>Modelo de recursos de computação
diagnóstico de tooenable num recurso de computação, por exemplo uma Máquina Virtual ou cluster do Service Fabric, terá de:

1. Adicione definição de recurso VM extensão toohello Olá diagnósticos do Azure.
2. Especifique um concentrador de conta e/ou evento de armazenamento como um parâmetro.
3. Adicione o conteúdo de Olá do ficheiro XML de WADCfg Olá XMLCfg propriedade, o escape todos os carateres XML corretamente.

> [!WARNING]
> Neste último passo pode ser tricky tooget direito. [Consulte este artigo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obter um exemplo que divisões Olá esquema de configuração de diagnósticos para variáveis de escape e formatadas corretamente.
> 
> 

Olá processo completo, incluindo exemplos, está descrito [neste documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Passos Seguintes
* [Leia mais sobre os registos de diagnóstico do Azure](monitoring-overview-of-diagnostic-logs.md)
* [Transmitir os registos de diagnóstico do Azure tooEvent Hubs](monitoring-stream-diagnostic-logs-to-event-hubs.md)

