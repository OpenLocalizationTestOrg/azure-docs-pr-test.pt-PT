---
title: disco do modelo toouse gerido de definir aaaConvert uma escala do Azure Resource Manager | Microsoft Docs
description: Converta um escala conjunto modelo tooa disco gerido escala definir o modelo.
keywords: "Conjuntos de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="63d71-104">Converter um escala conjunto modelo tooa disco gerido escala definir o modelo</span><span class="sxs-lookup"><span data-stu-id="63d71-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="63d71-105">Clientes com um modelo do Resource Manager para criar um conjunto não utilizar o disco gerido de dimensionamento podem desejar toomodify-toouse geridos disco.</span><span class="sxs-lookup"><span data-stu-id="63d71-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="63d71-106">Este artigo mostra como toodo esta, utilizando como um exemplo de um pedido de solicitação de Olá [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates), um repositório de Comunidade para modelos de Gestor de recursos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="63d71-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="63d71-107">pedido de solicitação completo de Olá pode ser visto aqui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e partes relevantes Olá Olá diff abaixo, juntamente com explicações:</span><span class="sxs-lookup"><span data-stu-id="63d71-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="63d71-108">Efetuar discos de SO Olá geridos</span><span class="sxs-lookup"><span data-stu-id="63d71-108">Making hello OS disks managed</span></span>

<span data-ttu-id="63d71-109">Diff de Olá abaixo, é possível ver que foi removido várias variáveis toostorage relacionados conta e o disco propriedades.</span><span class="sxs-lookup"><span data-stu-id="63d71-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="63d71-110">Tipo de conta de armazenamento já não é necessário (Standard_LRS é predefinido de Olá), mas foi ainda especificamos-lo se podemos wished para.</span><span class="sxs-lookup"><span data-stu-id="63d71-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="63d71-111">Apenas Standard_LRS Premium_LRS são suportados e com o disco gerido.</span><span class="sxs-lookup"><span data-stu-id="63d71-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="63d71-112">Novo sufixo de conta de armazenamento, a matriz de cadeia exclusiva e a contagem de sa eram utilizadas no Olá antigo modelo toogenerate armazenamento os nomes das contas.</span><span class="sxs-lookup"><span data-stu-id="63d71-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="63d71-113">Estas variáveis já não são necessárias no novo modelo de Olá porque o disco gerido cria automaticamente as contas de armazenamento em nome do cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="63d71-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="63d71-114">Da mesma forma, nome do contentor de vhd e nome do disco de SO já não são necessárias porque o disco gerido automaticamente os nomes de contentores de BLOBs de armazenamento subjacente Olá e os discos.</span><span class="sxs-lookup"><span data-stu-id="63d71-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="63d71-115">No Olá diff abaixo, iremos pode consulte atualizámos Olá computação api versão too2016-04-30-preview, que é Olá mais antiga versão necessária para suporte de disco gerido com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="63d71-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="63d71-116">Tenha em atenção de que foi ainda utilizamos discos não geridos na Olá nova api versão com sintaxe antiga Olá se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="63d71-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="63d71-117">Por outras palavras, se atualizamos apenas Olá versão da api de computação e não altere mais nada, modelo de Olá deve continuar toowork como antes.</span><span class="sxs-lookup"><span data-stu-id="63d71-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="63d71-118">Diff de Olá abaixo, é possível ver que estamos a remover recursos de conta de armazenamento Olá da matriz de recursos de Olá completamente.</span><span class="sxs-lookup"><span data-stu-id="63d71-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="63d71-119">Já não precisamos-los, uma vez que o disco gerido cria automaticamente em nosso nome.</span><span class="sxs-lookup"><span data-stu-id="63d71-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="63d71-120">Diff Olá abaixo, iremos pode ver que estamos a remover Olá depende cláusula referir-se de ciclo toohello de conjunto de dimensionamento de Olá que estava a criar contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="63d71-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="63d71-121">No modelo antigo Olá, isto foi se certificar de que as contas do storage Olá foram criadas antes do conjunto de dimensionamento de Olá teve início a criação, mas esta cláusula já não é necessária com disco gerido.</span><span class="sxs-lookup"><span data-stu-id="63d71-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="63d71-122">Podemos também remover a propriedade de contentores de vhd Olá e Olá propriedade de nome de disco de SO como estas propriedades são processadas automaticamente sob definições avançadas de Olá por disco gerido.</span><span class="sxs-lookup"><span data-stu-id="63d71-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="63d71-123">Se podemos wished, iremos adicionar `"managedDisk": { "storageAccountType": "Premium_LRS" }` na configuração de "osDisk" Olá se queremos discos de SO premium.</span><span class="sxs-lookup"><span data-stu-id="63d71-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="63d71-124">Apenas as VMs com uma maiúscula ou do minúscula ' Olá VM sku pode utilizar discos premium.</span><span class="sxs-lookup"><span data-stu-id="63d71-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="63d71-125">Não há nenhuma propriedade explícita na configuração de conjunto de dimensionamento de Olá para se toouse geridos ou disco não gerido.</span><span class="sxs-lookup"><span data-stu-id="63d71-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="63d71-126">conjunto de dimensionamento de Olá sabe qual toouse com base nas propriedades de Olá que estão presentes no perfil de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="63d71-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="63d71-127">Assim, é importante quando modificar Olá modelo tooensure destinadas a propriedades de direitos de Olá no perfil de armazenamento Olá do conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="63d71-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="63d71-128">discos de dados</span><span class="sxs-lookup"><span data-stu-id="63d71-128">Data disks</span></span>

<span data-ttu-id="63d71-129">Alterações de Olá acima, Olá escala conjunto utiliza gerido discos Olá SO disco, mas que acerca dos discos de dados? discos de dados de tooadd, Adicionar propriedade de "dataDisks" Olá "storageProfile" Olá mesmo nível, como "osDisk".</span><span class="sxs-lookup"><span data-stu-id="63d71-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="63d71-130">Olá valor da propriedade Olá é uma lista JSON de objetos, cada um dos quais tem propriedades "lun" (que tem de ser único por disco de dados numa VM), "createOption" ("vazio" está atualmente Olá só opção suportada) e "diskSizeGB" (Olá tamanho do disco de Olá em gigabytes; tem de ser maior que 0 e inferior a 1024) como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="63d71-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="63d71-131">Se especificar `n` esta matriz de discos, cada VM em escala Olá definir obtém `n` discos de dados.</span><span class="sxs-lookup"><span data-stu-id="63d71-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="63d71-132">Tenha em atenção, no entanto, se estes discos de dados são dispositivos sem formato.</span><span class="sxs-lookup"><span data-stu-id="63d71-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="63d71-133">Não estão formatados.</span><span class="sxs-lookup"><span data-stu-id="63d71-133">They are not formatted.</span></span> <span data-ttu-id="63d71-134">Está a funcionar toohello cliente tooattach, paritition e formato Olá discos antes de os utilizar.</span><span class="sxs-lookup"><span data-stu-id="63d71-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="63d71-135">Opcionalmente, pode também especificamos `"managedDisk": { "storageAccountType": "Premium_LRS" }` em cada toospecify de objeto de disco de dados que deve ser um disco de dados premium.</span><span class="sxs-lookup"><span data-stu-id="63d71-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="63d71-136">Apenas as VMs com uma maiúscula ou do minúscula ' Olá VM sku pode utilizar discos premium.</span><span class="sxs-lookup"><span data-stu-id="63d71-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="63d71-137">toolearn mais sobre a utilização de discos de dados com conjuntos de dimensionamento, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="63d71-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="63d71-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="63d71-138">Next steps</span></span>
<span data-ttu-id="63d71-139">Por exemplo modelos do Resource Manager utilizando conjuntos de dimensionamento, procure "vmss" no Olá [repositório do github de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="63d71-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="63d71-140">Para obter informações gerais, veja Olá [página de destino principal para conjuntos de dimensionamento](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="63d71-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

