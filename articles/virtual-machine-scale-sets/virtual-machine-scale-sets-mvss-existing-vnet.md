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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="170d9-103">Adicionar rede virtual existente referência tooan num modelo de conjunto de dimensionamento do Azure</span><span class="sxs-lookup"><span data-stu-id="170d9-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="170d9-104">Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toodeploy numa rede virtual existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="170d9-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="170d9-105">Altere a definição Olá modelo</span><span class="sxs-lookup"><span data-stu-id="170d9-105">Change hello template definition</span></span>

<span data-ttu-id="170d9-106">Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e o nosso modelo para implementar o dimensionamento de Olá definido numa rede virtual existente que pode ser visto [aqui](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="170d9-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="170d9-107">Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set existing-vnet`) peça a informação:</span><span class="sxs-lookup"><span data-stu-id="170d9-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="170d9-108">Em primeiro lugar, iremos adicionar um `subnetId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="170d9-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="170d9-109">Esta cadeia será transmitida para a configuração de conjunto de dimensionamento Olá, permitindo Olá conjunto de dimensionamento da sub-rede pré-criadas do tooidentify Olá toodeploy máquinas de virtuais em.</span><span class="sxs-lookup"><span data-stu-id="170d9-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="170d9-110">Esta cadeia deve ter o formato de Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="170d9-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="170d9-111">Por exemplo, o conjunto de dimensionamento de Olá toodeploy, numa rede virtual existente com o nome `myvnet`, sub-rede `mysubnet`, grupo de recursos `myrg`e subscrição `00000000-0000-0000-0000-000000000000`, Olá subnetId seria: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="170d9-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="170d9-112">Em seguida, iremos poder eliminar recursos de rede virtual Olá do Olá `resources` matriz, uma vez que vamos estiver a utilizar uma rede virtual existente e não precisa de toodeploy um novo.</span><span class="sxs-lookup"><span data-stu-id="170d9-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

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

<span data-ttu-id="170d9-113">rede virtual Olá já existe antes de implementar a modelo Olá, pelo que não existe nenhum toospecify necessidade de uma cláusula dependsOn da escala de Olá definidos toohello de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="170d9-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="170d9-114">Assim, vamos eliminar estas linhas:</span><span class="sxs-lookup"><span data-stu-id="170d9-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="170d9-115">Por fim, podemos passa Olá `subnetId` parâmetro definido pelo utilizador Olá (em vez de utilizar `resourceId` tooget id Olá uma vnet na Olá does de implementação do mesma, que é a escala de viável mínimo que Olá definida como modelo).</span><span class="sxs-lookup"><span data-stu-id="170d9-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="170d9-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="170d9-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
