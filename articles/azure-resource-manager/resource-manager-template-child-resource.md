---
title: recurso de subordinados aaaDefine no modelo do Azure | Microsoft Docs
description: "Mostra como tooset Olá tipo de recurso e o nome do recurso de subordinados de um modelo Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Definir nome e tipo de recurso subordinado no modelo do Resource Manager
Quando criar um modelo, terá de frequentemente tooinclude um recurso de subordinados que tooa relacionados principal recursos. Por exemplo, o seu modelo pode incluir um SQL server e uma base de dados. Olá SQL server é o recurso de principal de Olá, não sendo a base de dados de Olá recursos subordinados de Olá. 

formato de Olá do tipo de recurso subordinado Olá é:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

formato de Olá do nome do recurso Olá subordinado é:`{parent-resource-name}/{child-resource-name}`

No entanto, especifique o tipo de Olá e o nome num modelo de forma diferente com base na se está aninhado num recurso de principal de Olá, ou no seu próprio no nível superior Olá. Este tópico mostra como se aproxima toohandle ambas.

Quando construir um recurso de tooa referência completamente qualificado, Olá ordem toocombine segmentos de tipo de Olá e o nome não é simplesmente uma concatenação Olá dois.  Em vez disso, depois de espaço de nomes de Olá, utilize uma sequência de *nome do tipo* pares de menos específico toomost específico:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Por exemplo:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`está correto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` não está correto

## <a name="nested-child-resource"></a>Recurso subordinado aninhado
Olá toodefine da forma mais fácil um recurso subordinado é toonest-lo no recurso de principal de Olá. Olá exemplo seguinte mostra uma base de dados do SQL Server aninhado no SQL Server.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Para o recurso de subordinados Olá, Olá tipo se encontra definido demasiado`databases` , mas o respetivo tipo de recurso completo é `Microsoft.Sql/servers/databases`. Não fornecem `Microsoft.Sql/servers/` porque é suposto Olá principal do tipo de recurso. nome de recurso de subordinados de Olá está definido demasiado`exampledatabase` , mas o nome completo Olá inclui o nome do principal de Olá. Não fornecem `exampleserver` porque é suposto do recurso do Olá principal.

## <a name="top-level-child-resource"></a>Recurso de nível superior de subordinados
Pode definir os recursos subordinados de Olá no nível superior Olá. Poderá utilizar esta abordagem se o recurso do Olá principal não está implementado na Olá mesmo modelo ou, se pretender toouse `copy` toocreate vários recursos subordinados. Com esta abordagem, tem de fornecer o tipo de recurso completo Olá e incluem o nome de recurso principal Olá no nome do recurso Olá subordinado.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

base de dados de Olá é um servidor de toohello de recursos de subordinados, embora são definidos no mesmo nível de modelo de Olá de Olá.

## <a name="next-steps"></a>Passos seguintes
* Para ver as recomendações sobre como toocreate modelos, consulte [melhores práticas para a criação de modelos Azure Resource Manager](resource-manager-template-best-practices.md).
* Para obter um exemplo de criação subordinado vários recursos, consulte [implementar várias instâncias de recursos em modelos do Azure Resource Manager](resource-group-create-multiple.md).
