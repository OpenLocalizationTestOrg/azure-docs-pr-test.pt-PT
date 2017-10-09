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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="7d752-103">Adicionar que tooan uma imagem personalizada do Azure escala definir modelo</span><span class="sxs-lookup"><span data-stu-id="7d752-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="7d752-104">Este artigo mostra como toomodify Olá [modelo de conjunto de dimensionamento viável mínimo](./virtual-machine-scale-sets-mvss-start.md) toodeploy da imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="7d752-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="7d752-105">Altere a definição Olá modelo</span><span class="sxs-lookup"><span data-stu-id="7d752-105">Change hello template definition</span></span>

<span data-ttu-id="7d752-106">Pode ser visto o nosso modelo de conjunto mínimo de escala viável [aqui](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), e pode ser visto o nosso modelo para implementar o conjunto de uma imagem personalizada de dimensionamento de Olá [aqui](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7d752-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="7d752-107">Vamos examinar Olá diff utilizado toocreate este modelo (`git diff minimum-viable-scale-set custom-image`) peça a informação:</span><span class="sxs-lookup"><span data-stu-id="7d752-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="7d752-108">Criar uma imagem de disco gerido</span><span class="sxs-lookup"><span data-stu-id="7d752-108">Creating a managed disk image</span></span>

<span data-ttu-id="7d752-109">Se já tiver uma imagem de disco gerido personalizado (um recurso do tipo `Microsoft.Compute/images`), em seguida, pode ignorar esta secção.</span><span class="sxs-lookup"><span data-stu-id="7d752-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="7d752-110">Em primeiro lugar, iremos adicionar um `sourceImageVhdUri` parâmetro, que é Olá URI toohello generalizado blob no Storage do Azure que contém Olá toodeploy de imagem personalizada do.</span><span class="sxs-lookup"><span data-stu-id="7d752-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="7d752-111">Em seguida, iremos adicionar um recurso do tipo `Microsoft.Compute/images`que imagem de disco gerido Olá baseia-se no blob Olá generalizado localizado em URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="7d752-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="7d752-112">Esta imagem tem de constar Olá mesma região que o conjunto de dimensionamento de Olá que o utiliza.</span><span class="sxs-lookup"><span data-stu-id="7d752-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="7d752-113">Nas propriedades de Olá da imagem de Olá, especificamos tipo Olá SO, localização Olá do blob Olá (de Olá `sourceImageVhdUri` parâmetro) e o tipo de conta de armazenamento Olá:</span><span class="sxs-lookup"><span data-stu-id="7d752-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="7d752-114">No Olá conjunto de dimensionamento de recurso, iremos adicionar um `dependsOn` cláusula toohello imagem personalizada toomake se a imagem de Olá é criada antes do conjunto de dimensionamento de Olá tenta toodeploy partir dessa imagem de referência:</span><span class="sxs-lookup"><span data-stu-id="7d752-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="7d752-115">Imagem de disco gerido do propriedades toouse Olá do conjunto de dimensionamento de alteração</span><span class="sxs-lookup"><span data-stu-id="7d752-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="7d752-116">No Olá `imageReference` da escala de Olá definir `storageProfile`, em vez de especificar Olá publicador, oferta, sku e a versão de uma imagem de plataforma, especificamos Olá `id` de Olá `Microsoft.Compute/images` recursos:</span><span class="sxs-lookup"><span data-stu-id="7d752-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="7d752-117">Neste exemplo, utilizamos Olá `resourceId` função tooget Olá ID de recurso da imagem de Olá criado no Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="7d752-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="7d752-118">Se tiver criado a imagem de disco gerido Olá previamente, deve fornecer id Olá dessa imagem em vez disso.</span><span class="sxs-lookup"><span data-stu-id="7d752-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="7d752-119">Este id tem de ser do formulário Olá: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="7d752-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7d752-120">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="7d752-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
