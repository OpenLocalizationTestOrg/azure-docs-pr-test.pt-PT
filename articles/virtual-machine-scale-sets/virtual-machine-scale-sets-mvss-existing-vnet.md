---
title: "Referência a uma rede virtual existente num modelo de conjunto de dimensionamento do Azure | Microsoft Docs"
description: "Saiba como tooadd a virtual rede tooan modelo de conjunto de dimensionamento de Máquina Virtual do Azure existente"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Adicionar rede virtual existente referência tooan num modelo de conjunto de dimensionamento do Azure

Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toodeploy numa rede virtual existente em vez de criar um novo.

## <a name="change-hello-template-definition"></a>Altere a definição Olá modelo

Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e o nosso modelo para implementar o dimensionamento de Olá definido numa rede virtual existente que pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) peça a informação:

Em primeiro lugar, iremos adicionar um `subnetId` parâmetro. Esta cadeia será transmitida para a configuração de conjunto de dimensionamento Olá, permitindo Olá conjunto de dimensionamento da sub-rede pré-criadas do tooidentify Olá toodeploy máquinas de virtuais em. Esta cadeia deve ter o formato de Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Por exemplo, o conjunto de dimensionamento de Olá toodeploy, numa rede virtual existente com o nome `myvnet`, sub-rede `mysubnet`, grupo de recursos `myrg`e subscrição `00000000-0000-0000-0000-000000000000`, Olá subnetId seria: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

Em seguida, iremos poder eliminar recursos de rede virtual Olá do Olá `resources` matriz, uma vez que vamos estiver a utilizar uma rede virtual existente e não precisa de toodeploy um novo.

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

rede virtual Olá já existe antes de implementar a modelo Olá, pelo que não existe nenhum toospecify necessidade de uma cláusula dependsOn da escala de Olá definidos toohello de rede virtual. Assim, vamos eliminar estas linhas:

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

Por fim, podemos passa Olá `subnetId` parâmetro definido pelo utilizador Olá (em vez de utilizar `resourceId` tooget id Olá uma vnet na Olá does de implementação do mesma, que é a escala de viável mínimo que Olá definida como modelo).

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>Passos seguintes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
