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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Converter um escala conjunto modelo tooa disco gerido escala definir o modelo

Clientes com um modelo do Resource Manager para criar um conjunto não utilizar o disco gerido de dimensionamento podem desejar toomodify-toouse geridos disco. Este artigo mostra como toodo esta, utilizando como um exemplo de um pedido de solicitação de Olá [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates), um repositório de Comunidade para modelos de Gestor de recursos de exemplo. pedido de solicitação completo de Olá pode ser visto aqui: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), e partes relevantes Olá Olá diff abaixo, juntamente com explicações:

## <a name="making-hello-os-disks-managed"></a>Efetuar discos de SO Olá geridos

Diff de Olá abaixo, é possível ver que foi removido várias variáveis toostorage relacionados conta e o disco propriedades. Tipo de conta de armazenamento já não é necessário (Standard_LRS é predefinido de Olá), mas foi ainda especificamos-lo se podemos wished para. Apenas Standard_LRS Premium_LRS são suportados e com o disco gerido. Novo sufixo de conta de armazenamento, a matriz de cadeia exclusiva e a contagem de sa eram utilizadas no Olá antigo modelo toogenerate armazenamento os nomes das contas. Estas variáveis já não são necessárias no novo modelo de Olá porque o disco gerido cria automaticamente as contas de armazenamento em nome do cliente Olá. Da mesma forma, nome do contentor de vhd e nome do disco de SO já não são necessárias porque o disco gerido automaticamente os nomes de contentores de BLOBs de armazenamento subjacente Olá e os discos.

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


No Olá diff abaixo, iremos pode consulte atualizámos Olá computação api versão too2016-04-30-preview, que é Olá mais antiga versão necessária para suporte de disco gerido com conjuntos de dimensionamento. Tenha em atenção de que foi ainda utilizamos discos não geridos na Olá nova api versão com sintaxe antiga Olá se assim o desejar. Por outras palavras, se atualizamos apenas Olá versão da api de computação e não altere mais nada, modelo de Olá deve continuar toowork como antes.

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

Diff de Olá abaixo, é possível ver que estamos a remover recursos de conta de armazenamento Olá da matriz de recursos de Olá completamente. Já não precisamos-los, uma vez que o disco gerido cria automaticamente em nosso nome.

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

Diff Olá abaixo, iremos pode ver que estamos a remover Olá depende cláusula referir-se de ciclo toohello de conjunto de dimensionamento de Olá que estava a criar contas de armazenamento. No modelo antigo Olá, isto foi se certificar de que as contas do storage Olá foram criadas antes do conjunto de dimensionamento de Olá teve início a criação, mas esta cláusula já não é necessária com disco gerido. Podemos também remover a propriedade de contentores de vhd Olá e Olá propriedade de nome de disco de SO como estas propriedades são processadas automaticamente sob definições avançadas de Olá por disco gerido. Se podemos wished, iremos adicionar `"managedDisk": { "storageAccountType": "Premium_LRS" }` na configuração de "osDisk" Olá se queremos discos de SO premium. Apenas as VMs com uma maiúscula ou do minúscula ' Olá VM sku pode utilizar discos premium.

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

Não há nenhuma propriedade explícita na configuração de conjunto de dimensionamento de Olá para se toouse geridos ou disco não gerido. conjunto de dimensionamento de Olá sabe qual toouse com base nas propriedades de Olá que estão presentes no perfil de armazenamento Olá. Assim, é importante quando modificar Olá modelo tooensure destinadas a propriedades de direitos de Olá no perfil de armazenamento Olá do conjunto de dimensionamento de Olá.


## <a name="data-disks"></a>discos de dados

Alterações de Olá acima, Olá escala conjunto utiliza gerido discos Olá SO disco, mas que acerca dos discos de dados? discos de dados de tooadd, Adicionar propriedade de "dataDisks" Olá "storageProfile" Olá mesmo nível, como "osDisk". Olá valor da propriedade Olá é uma lista JSON de objetos, cada um dos quais tem propriedades "lun" (que tem de ser único por disco de dados numa VM), "createOption" ("vazio" está atualmente Olá só opção suportada) e "diskSizeGB" (Olá tamanho do disco de Olá em gigabytes; tem de ser maior que 0 e inferior a 1024) como no seguinte exemplo de Olá: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Se especificar `n` esta matriz de discos, cada VM em escala Olá definir obtém `n` discos de dados. Tenha em atenção, no entanto, se estes discos de dados são dispositivos sem formato. Não estão formatados. Está a funcionar toohello cliente tooattach, paritition e formato Olá discos antes de os utilizar. Opcionalmente, pode também especificamos `"managedDisk": { "storageAccountType": "Premium_LRS" }` em cada toospecify de objeto de disco de dados que deve ser um disco de dados premium. Apenas as VMs com uma maiúscula ou do minúscula ' Olá VM sku pode utilizar discos premium.

toolearn mais sobre a utilização de discos de dados com conjuntos de dimensionamento, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Passos seguintes
Por exemplo modelos do Resource Manager utilizando conjuntos de dimensionamento, procure "vmss" no Olá [repositório do github de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).

Para obter informações gerais, veja Olá [página de destino principal para conjuntos de dimensionamento](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

