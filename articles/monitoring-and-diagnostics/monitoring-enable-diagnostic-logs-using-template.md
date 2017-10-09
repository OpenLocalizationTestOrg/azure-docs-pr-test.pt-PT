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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="5beb9-103">Ativar automaticamente definições de diagnóstico durante a criação de recursos através de um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5beb9-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="5beb9-104">Neste artigo mostramos como pode utilizar um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure definições de diagnóstico num recurso quando é criado.</span><span class="sxs-lookup"><span data-stu-id="5beb9-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="5beb9-105">Isto permite-lhe iniciar tooautomatically sua tooEvent métricas e registos de diagnóstico Hubs, arquivá-los numa conta de armazenamento ou enviar-lhes tooLog análise quando é criado um recurso de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="5beb9-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="5beb9-106">método de Olá para ativar os registos de diagnóstico com um modelo do Resource Manager depende do tipo de recurso Olá.</span><span class="sxs-lookup"><span data-stu-id="5beb9-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="5beb9-107">**Computação não** recursos (por exemplo, grupos de segurança de rede, as Logic Apps, automatização) [definições de diagnóstico descrito neste artigo](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="5beb9-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="5beb9-108">**Computação** recursos (WAD/LAD baseado) utilizam Olá [ficheiro de configuração de WAD/LAD descrito neste artigo](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="5beb9-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="5beb9-109">Este artigo descreve como os diagnósticos de tooconfigure utilizando um dos métodos.</span><span class="sxs-lookup"><span data-stu-id="5beb9-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="5beb9-110">os passos básicos de Olá são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5beb9-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="5beb9-111">Crie um modelo como um ficheiro JSON que descreve como toocreate Olá recursos e ative os diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="5beb9-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="5beb9-112">[Implementar a modelo Olá com qualquer método de implementação](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5beb9-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="5beb9-113">Abaixo que lhe damos um exemplo de modelo de Olá ficheiro JSON tem toogenerate de não computação e de recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="5beb9-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="5beb9-114">Modelo de recursos de computação não</span><span class="sxs-lookup"><span data-stu-id="5beb9-114">Non-Compute resource template</span></span>
<span data-ttu-id="5beb9-115">Não-recursos de computação, terá de toodo duas coisas:</span><span class="sxs-lookup"><span data-stu-id="5beb9-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="5beb9-116">Adicione o blob de parâmetros de toohello parâmetros para o nome de conta do storage Olá, ID de regra de barramento de serviço e/ou ID da área de trabalho de análise de registos do OMS (ativar o arquivo de registos de diagnóstico numa conta do storage, transmissão em fluxo de registos tooEvent Hubs e/ou envio de registos tooLog análise).</span><span class="sxs-lookup"><span data-stu-id="5beb9-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
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
2. <span data-ttu-id="5beb9-117">Na matriz de recursos de Olá do recurso de Olá para o qual pretende que os registos de diagnóstico tooenable, adicione um recurso do tipo `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="5beb9-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="5beb9-118">Olá blob de propriedades para a definição de diagnóstico de Olá segue [formato Olá descrito neste artigo](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="5beb9-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="5beb9-119">Adicionar Olá `metrics` propriedade permitirá toothese métricas tooalso envio recursos mesmo produz, fornecido que [recursos Olá suporta métricas de Monitor de Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5beb9-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="5beb9-120">Eis um exemplo completo que cria uma aplicação lógica e ativa a transmissão em fluxo tooEvent Hubs e armazenamento numa conta do storage.</span><span class="sxs-lookup"><span data-stu-id="5beb9-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

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

## <a name="compute-resource-template"></a><span data-ttu-id="5beb9-121">Modelo de recursos de computação</span><span class="sxs-lookup"><span data-stu-id="5beb9-121">Compute resource template</span></span>
<span data-ttu-id="5beb9-122">diagnóstico de tooenable num recurso de computação, por exemplo uma Máquina Virtual ou cluster do Service Fabric, terá de:</span><span class="sxs-lookup"><span data-stu-id="5beb9-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="5beb9-123">Adicione definição de recurso VM extensão toohello Olá diagnósticos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5beb9-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="5beb9-124">Especifique um concentrador de conta e/ou evento de armazenamento como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5beb9-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="5beb9-125">Adicione o conteúdo de Olá do ficheiro XML de WADCfg Olá XMLCfg propriedade, o escape todos os carateres XML corretamente.</span><span class="sxs-lookup"><span data-stu-id="5beb9-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="5beb9-126">Neste último passo pode ser tricky tooget direito.</span><span class="sxs-lookup"><span data-stu-id="5beb9-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="5beb9-127">[Consulte este artigo](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) para obter um exemplo que divisões Olá esquema de configuração de diagnósticos para variáveis de escape e formatadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="5beb9-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="5beb9-128">Olá processo completo, incluindo exemplos, está descrito [neste documento](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5beb9-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5beb9-129">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="5beb9-129">Next Steps</span></span>
* [<span data-ttu-id="5beb9-130">Leia mais sobre os registos de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="5beb9-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="5beb9-131">Transmitir os registos de diagnóstico do Azure tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="5beb9-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

