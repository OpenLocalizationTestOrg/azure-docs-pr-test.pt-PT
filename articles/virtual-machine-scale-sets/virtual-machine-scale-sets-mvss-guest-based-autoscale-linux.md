---
title: "Utilize o dimensionamento automático do Azure com a métrica de convidado num modelo de conjunto de dimensionamento do Linux | Microsoft Docs"
description: "Saiba como tooautoscale através de métricas de convidado num modelo de conjunto de dimensionamento de Máquina Virtual do Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="8865b-103">Dimensionamento automático através de métricas de convidado num modelo de conjunto de dimensionamento do Linux</span><span class="sxs-lookup"><span data-stu-id="8865b-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="8865b-104">Existem dois tipos de métricas no Azure que estão reunidas a partir de VMs e conjuntos de dimensionamento: alguns provenientes de Olá anfitrião VM e outras pessoas vêm da VM do convidado de Olá.</span><span class="sxs-lookup"><span data-stu-id="8865b-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="8865b-105">Métricas de anfitrião não necessitam de configuração adicional porque estes não são recolhidos pelo anfitrião Olá VM, enquanto que necessitam de métricas de convidado nos tooinstall Olá [extensão do Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) ou Olá [Linux do diagnóstico do Azure extensão](../virtual-machines/linux/diagnostic-extension.md) no Olá VM de convidado.</span><span class="sxs-lookup"><span data-stu-id="8865b-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="8865b-106">Um comuns razão toouse convidado métricas em vez de métricas de anfitrião é que as métricas de convidado fornecem uma seleção maior das métricas de métricas de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="8865b-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="8865b-107">Um exemplo desse tipo é métricas do consumo de memória, que só estão disponíveis através de métricas de convidado.</span><span class="sxs-lookup"><span data-stu-id="8865b-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="8865b-108">métricas de anfitriões de Olá suportado estão listadas [aqui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e as métricas frequentemente utilizadas convidado são listadas [aqui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8865b-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="8865b-109">Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toouse regras de dimensionamento automático com base nas métricas de convidado para conjuntos de dimensionamento do Linux.</span><span class="sxs-lookup"><span data-stu-id="8865b-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="8865b-110">Altere a definição Olá modelo</span><span class="sxs-lookup"><span data-stu-id="8865b-110">Change hello template definition</span></span>

<span data-ttu-id="8865b-111">Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e pode ser visto o nosso modelo para implementar o conjunto com dimensionamento automático baseada no convidado de dimensionamento do Linux Olá [aqui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="8865b-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="8865b-112">Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) peça a informação:</span><span class="sxs-lookup"><span data-stu-id="8865b-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="8865b-113">Em primeiro lugar, iremos adicionar parâmetros para `storageAccountName` e `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="8865b-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="8865b-114">agente de diagnóstico de Olá irá armazenar os dados métricos num [tabela](../cosmos-db/table-storage-how-to-use-dotnet.md) nesta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8865b-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="8865b-115">A partir de Olá versão 3.0 do agente de diagnóstico de Linux, utilizar uma chave de acesso de armazenamento já não é suportada.</span><span class="sxs-lookup"><span data-stu-id="8865b-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="8865b-116">Iremos tem de utilizar um [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="8865b-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

<span data-ttu-id="8865b-117">Em seguida, iremos modificar o conjunto de dimensionamento de Olá `extensionProfile` extensão de diagnóstico de Olá tooinclude.</span><span class="sxs-lookup"><span data-stu-id="8865b-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="8865b-118">Nesta configuração, iremos especificar recursos Olá toocollect métricas de definido o ID do dimensionamento Olá, bem como Olá conta de armazenamento e as métricas do SAS token toouse toostore Olá.</span><span class="sxs-lookup"><span data-stu-id="8865b-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="8865b-119">Também iremos especificar frequência métricas Olá são agregadas (neste caso, cada minuto) e que tootrack métricas (neste cenário memória utilizada por cento).</span><span class="sxs-lookup"><span data-stu-id="8865b-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="8865b-120">Para obter informações mais detalhadas sobre esta configuração e métricas que não seja a percentagem de memória utilizada, consulte [esta documentação](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8865b-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

<span data-ttu-id="8865b-121">Por último, iremos adicionar um `autoscaleSettings` dimensionamento automático de tooconfigure de recursos com base nestas métricas.</span><span class="sxs-lookup"><span data-stu-id="8865b-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="8865b-122">Este recurso tem um `dependsOn` cláusula que faça referência a escala de Olá definir tooensure que conjunto de dimensionamento de Olá existe antes de tentar tooautoscale-lo.</span><span class="sxs-lookup"><span data-stu-id="8865b-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="8865b-123">Vamos escolher um tooautoscale métrica diferentes no, utilizamos Olá `counterSpecifier` da configuração de extensão de diagnóstico Olá como Olá `metricName` na configuração de dimensionamento automático de Olá.</span><span class="sxs-lookup"><span data-stu-id="8865b-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="8865b-124">Para obter mais informações sobre a configuração de dimensionamento automático, consulte Olá [melhores práticas de dimensionamento automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) e Olá [documentação de referência da API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="8865b-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a><span data-ttu-id="8865b-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8865b-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
