---
title: "Referência a uma imagem personalizada num modelo de conjunto de dimensionamento do Azure | Microsoft Docs"
description: "Saiba como tooadd personalizadas imagem tooan modelo de conjunto de dimensionamento de Máquina Virtual do Azure existente"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Adicionar que tooan uma imagem personalizada do Azure escala definir modelo

Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toodeploy da imagem personalizada.

## <a name="change-hello-template-definition"></a>Altere a definição Olá modelo

Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e pode ser visto o nosso modelo para implementar o conjunto de uma imagem personalizada de dimensionamento de Olá [aqui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set custom-image`) peça a informação:

### <a name="creating-a-managed-disk-image"></a>Criar uma imagem de disco gerido

Se já tiver uma imagem de disco gerido personalizado (um recurso do tipo `Microsoft.Compute/images`), em seguida, pode ignorar esta secção.

Em primeiro lugar, iremos adicionar um `sourceImageVhdUri` parâmetro, que é Olá URI toohello generalizado blob no Storage do Azure que contém Olá toodeploy de imagem personalizada do.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Em seguida, iremos adicionar um recurso do tipo `Microsoft.Compute/images`que imagem de disco gerido Olá baseia-se no blob Olá generalizado localizado em URI `sourceImageVhdUri`. Esta imagem tem de constar Olá mesma região que o conjunto de dimensionamento de Olá que o utiliza. Nas propriedades de Olá da imagem de Olá, especificamos tipo Olá SO, localização Olá do blob Olá (de Olá `sourceImageVhdUri` parâmetro) e o tipo de conta de armazenamento Olá:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

No Olá conjunto de dimensionamento de recurso, iremos adicionar um `dependsOn` cláusula toohello imagem personalizada toomake se a imagem de Olá é criada antes do conjunto de dimensionamento de Olá tenta toodeploy partir dessa imagem de referência:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Imagem de disco gerido do propriedades toouse Olá do conjunto de dimensionamento de alteração

No Olá `imageReference` da escala de Olá definir `storageProfile`, em vez de especificar Olá publicador, oferta, sku e a versão de uma imagem de plataforma, especificamos Olá `id` de Olá `Microsoft.Compute/images` recursos:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

Neste exemplo, utilizamos Olá `resourceId` função tooget Olá ID de recurso da imagem de Olá criado no Olá mesmo modelo. Se tiver criado a imagem de disco gerido Olá previamente, deve fornecer id Olá dessa imagem em vez disso. Este id tem de ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Passos Seguintes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
