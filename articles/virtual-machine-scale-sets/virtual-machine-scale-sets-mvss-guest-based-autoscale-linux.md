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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Dimensionamento automático através de métricas de convidado num modelo de conjunto de dimensionamento do Linux

Existem dois tipos de métricas no Azure que estão reunidas a partir de VMs e conjuntos de dimensionamento: alguns provenientes de Olá anfitrião VM e outras pessoas vêm da VM do convidado de Olá. Métricas de anfitrião não necessitam de configuração adicional porque estes não são recolhidos pelo anfitrião Olá VM, enquanto que necessitam de métricas de convidado nos tooinstall Olá [extensão do Windows Azure Diagnostics](../virtual-machines/windows/extensions-diagnostics-template.md) ou Olá [Linux do diagnóstico do Azure extensão](../virtual-machines/linux/diagnostic-extension.md) no Olá VM de convidado. Um comuns razão toouse convidado métricas em vez de métricas de anfitrião é que as métricas de convidado fornecem uma seleção maior das métricas de métricas de anfitrião. Um exemplo desse tipo é métricas do consumo de memória, que só estão disponíveis através de métricas de convidado. métricas de anfitriões de Olá suportado estão listadas [aqui](../monitoring-and-diagnostics/monitoring-supported-metrics.md), e as métricas frequentemente utilizadas convidado são listadas [aqui](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toouse regras de dimensionamento automático com base nas métricas de convidado para conjuntos de dimensionamento do Linux.

## <a name="change-hello-template-definition"></a>Altere a definição Olá modelo

Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e pode ser visto o nosso modelo para implementar o conjunto com dimensionamento automático baseada no convidado de dimensionamento do Linux Olá [aqui](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) peça a informação:

Em primeiro lugar, iremos adicionar parâmetros para `storageAccountName` e `storageAccountSasToken`. agente de diagnóstico de Olá irá armazenar os dados métricos num [tabela](../cosmos-db/table-storage-how-to-use-dotnet.md) nesta conta de armazenamento. A partir de Olá versão 3.0 do agente de diagnóstico de Linux, utilizar uma chave de acesso de armazenamento já não é suportada. Iremos tem de utilizar um [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

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

Em seguida, iremos modificar o conjunto de dimensionamento de Olá `extensionProfile` extensão de diagnóstico de Olá tooinclude. Nesta configuração, iremos especificar recursos Olá toocollect métricas de definido o ID do dimensionamento Olá, bem como Olá conta de armazenamento e as métricas do SAS token toouse toostore Olá. Também iremos especificar frequência métricas Olá são agregadas (neste caso, cada minuto) e que tootrack métricas (neste cenário memória utilizada por cento). Para obter informações mais detalhadas sobre esta configuração e métricas que não seja a percentagem de memória utilizada, consulte [esta documentação](../virtual-machines/linux/diagnostic-extension.md).

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

Por último, iremos adicionar um `autoscaleSettings` dimensionamento automático de tooconfigure de recursos com base nestas métricas. Este recurso tem um `dependsOn` cláusula que faça referência a escala de Olá definir tooensure que conjunto de dimensionamento de Olá existe antes de tentar tooautoscale-lo. Vamos escolher um tooautoscale métrica diferentes no, utilizamos Olá `counterSpecifier` da configuração de extensão de diagnóstico Olá como Olá `metricName` na configuração de dimensionamento automático de Olá. Para obter mais informações sobre a configuração de dimensionamento automático, consulte Olá [melhores práticas de dimensionamento automático](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) e Olá [documentação de referência da API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931928.aspx).

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





## <a name="next-steps"></a>Passos seguintes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
