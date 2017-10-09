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
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="92688-103">Definir nome e tipo de recurso subordinado no modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92688-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="92688-104">Quando criar um modelo, terá de frequentemente tooinclude um recurso de subordinados que tooa relacionados principal recursos.</span><span class="sxs-lookup"><span data-stu-id="92688-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="92688-105">Por exemplo, o seu modelo pode incluir um SQL server e uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="92688-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="92688-106">Olá SQL server é o recurso de principal de Olá, não sendo a base de dados de Olá recursos subordinados de Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="92688-107">formato de Olá do tipo de recurso subordinado Olá é:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="92688-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="92688-108">formato de Olá do nome do recurso Olá subordinado é:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="92688-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="92688-109">No entanto, especifique o tipo de Olá e o nome num modelo de forma diferente com base na se está aninhado num recurso de principal de Olá, ou no seu próprio no nível superior Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="92688-110">Este tópico mostra como se aproxima toohandle ambas.</span><span class="sxs-lookup"><span data-stu-id="92688-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="92688-111">Quando construir um recurso de tooa referência completamente qualificado, Olá ordem toocombine segmentos de tipo de Olá e o nome não é simplesmente uma concatenação Olá dois.</span><span class="sxs-lookup"><span data-stu-id="92688-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="92688-112">Em vez disso, depois de espaço de nomes de Olá, utilize uma sequência de *nome do tipo* pares de menos específico toomost específico:</span><span class="sxs-lookup"><span data-stu-id="92688-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="92688-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="92688-113">For example:</span></span>

<span data-ttu-id="92688-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`está correto `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` não está correto</span><span class="sxs-lookup"><span data-stu-id="92688-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="92688-115">Recurso subordinado aninhado</span><span class="sxs-lookup"><span data-stu-id="92688-115">Nested child resource</span></span>
<span data-ttu-id="92688-116">Olá toodefine da forma mais fácil um recurso subordinado é toonest-lo no recurso de principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="92688-117">Olá exemplo seguinte mostra uma base de dados do SQL Server aninhado no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="92688-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="92688-118">Para o recurso de subordinados Olá, Olá tipo se encontra definido demasiado`databases` , mas o respetivo tipo de recurso completo é `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="92688-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="92688-119">Não fornecem `Microsoft.Sql/servers/` porque é suposto Olá principal do tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="92688-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="92688-120">nome de recurso de subordinados de Olá está definido demasiado`exampledatabase` , mas o nome completo Olá inclui o nome do principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="92688-121">Não fornecem `exampleserver` porque é suposto do recurso do Olá principal.</span><span class="sxs-lookup"><span data-stu-id="92688-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="92688-122">Recurso de nível superior de subordinados</span><span class="sxs-lookup"><span data-stu-id="92688-122">Top-level child resource</span></span>
<span data-ttu-id="92688-123">Pode definir os recursos subordinados de Olá no nível superior Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="92688-124">Poderá utilizar esta abordagem se o recurso do Olá principal não está implementado na Olá mesmo modelo ou, se pretender toouse `copy` toocreate vários recursos subordinados.</span><span class="sxs-lookup"><span data-stu-id="92688-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="92688-125">Com esta abordagem, tem de fornecer o tipo de recurso completo Olá e incluem o nome de recurso principal Olá no nome do recurso Olá subordinado.</span><span class="sxs-lookup"><span data-stu-id="92688-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="92688-126">base de dados de Olá é um servidor de toohello de recursos de subordinados, embora são definidos no mesmo nível de modelo de Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="92688-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92688-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="92688-127">Next steps</span></span>
* <span data-ttu-id="92688-128">Para ver as recomendações sobre como toocreate modelos, consulte [melhores práticas para a criação de modelos Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="92688-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="92688-129">Para obter um exemplo de criação subordinado vários recursos, consulte [implementar várias instâncias de recursos em modelos do Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="92688-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
