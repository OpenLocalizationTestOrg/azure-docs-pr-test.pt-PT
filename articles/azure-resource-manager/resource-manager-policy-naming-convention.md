---
title: "as políticas de recursos de aaaAzure para as convenções de nomenclatura | Microsoft Docs"
description: "Descreve as políticas do Azure Resource Manager para as convenções de nomenclatura de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="d71bd-103">Aplicar políticas de recursos de nomes e texto</span><span class="sxs-lookup"><span data-stu-id="d71bd-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="d71bd-104">Este tópico mostra várias [as políticas de recursos](resource-manager-policy.md) pode aplicar tooestablish convenções de atribuição de nomes e texto.</span><span class="sxs-lookup"><span data-stu-id="d71bd-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="d71bd-105">Estas políticas garantir consistência para os nomes de recursos e valores de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="d71bd-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="d71bd-106">Definir a Convenção de nomenclatura com carateres universais</span><span class="sxs-lookup"><span data-stu-id="d71bd-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="d71bd-107">Olá exemplo seguinte mostra Olá utilização do caráter universal, que é suportado pelo Olá **como** condição.</span><span class="sxs-lookup"><span data-stu-id="d71bd-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="d71bd-108">Olá condição Estados que se hello nome corresponde ao padrão mencionadas Olá (namePrefix\*nameSuffix) negar o pedido de Olá:</span><span class="sxs-lookup"><span data-stu-id="d71bd-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="d71bd-109">Definir a Convenção de nomenclatura com o padrão</span><span class="sxs-lookup"><span data-stu-id="d71bd-109">Set naming convention with pattern</span></span>

<span data-ttu-id="d71bd-110">toospecify que os nomes de recursos correspondem um padrão, utilize Olá correspondem à condição.</span><span class="sxs-lookup"><span data-stu-id="d71bd-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="d71bd-111">Olá seguinte exemplo requer nomes toostart com `contoso` e conter seis letras adicionais:</span><span class="sxs-lookup"><span data-stu-id="d71bd-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="d71bd-112">Padrão de data de conjunto para o valor da etiqueta</span><span class="sxs-lookup"><span data-stu-id="d71bd-112">Set date pattern for tag value</span></span>

<span data-ttu-id="d71bd-113">toorequire um padrão de data de dois dígitos, traço, três letras, dash e quatro dígitos, utilize:</span><span class="sxs-lookup"><span data-stu-id="d71bd-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d71bd-114">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d71bd-114">Next steps</span></span>
* <span data-ttu-id="d71bd-115">Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito.</span><span class="sxs-lookup"><span data-stu-id="d71bd-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="d71bd-116">âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="d71bd-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d71bd-117">políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d71bd-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d71bd-118">políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="d71bd-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="d71bd-119">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d71bd-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

