---
title: "as políticas de recursos de aaaAzure para etiquetas | Microsoft Docs"
description: "Fornece exemplos de políticas de recursos para gerir etiquetas de recursos"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="5c030-103">Aplicar políticas de recursos de etiquetas</span><span class="sxs-lookup"><span data-stu-id="5c030-103">Apply resource policies for tags</span></span>

<span data-ttu-id="5c030-104">Este tópico fornece as regras de política comum que pode aplicar a utilização consistente tooensure etiquetas nos recursos.</span><span class="sxs-lookup"><span data-stu-id="5c030-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="5c030-105">Aplicar um grupo de recursos de tooa de política de etiqueta ou uma subscrição com os recursos existentes não retroactively aplicam-se recursos de toothose Olá política.</span><span class="sxs-lookup"><span data-stu-id="5c030-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="5c030-106">políticas de Olá tooenforce esses recursos, acionar um toohello de atualização existente recursos.</span><span class="sxs-lookup"><span data-stu-id="5c030-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="5c030-107">Este artigo inclui um exemplo do PowerShell para acionar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="5c030-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="5c030-108">Certifique-se de que todos os recursos num grupo de recursos tem um tag/valor</span><span class="sxs-lookup"><span data-stu-id="5c030-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="5c030-109">Um requisito comum é que todos os recursos num grupo de recursos tem uma tag específica e o valor.</span><span class="sxs-lookup"><span data-stu-id="5c030-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="5c030-110">Este requisito é frequentemente necessário tootrack custos pelo departamento.</span><span class="sxs-lookup"><span data-stu-id="5c030-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="5c030-111">Olá seguintes condições deve ser cumprido:</span><span class="sxs-lookup"><span data-stu-id="5c030-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="5c030-112">Olá necessário etiqueta valor são toonew anexado e atualizar recursos que não tem tag de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c030-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="5c030-113">Olá necessário tag e valor não é possível remover quaisquer recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="5c030-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="5c030-114">Concretizar este requisito aplicando o grupo de recursos de tooa do duas políticas incorporadas.</span><span class="sxs-lookup"><span data-stu-id="5c030-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="5c030-115">ID</span><span class="sxs-lookup"><span data-stu-id="5c030-115">ID</span></span> | <span data-ttu-id="5c030-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="5c030-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="5c030-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="5c030-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="5c030-118">Aplica-se uma tag necessária e o respetivo valor predefinido se não for especificada pelo utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="5c030-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="5c030-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="5c030-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="5c030-120">Impõe uma tag necessária e o respetivo valor.</span><span class="sxs-lookup"><span data-stu-id="5c030-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="5c030-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c030-121">PowerShell</span></span>

<span data-ttu-id="5c030-122">Olá seguinte script do PowerShell atribui o grupo de recursos do Olá política incorporada duas definições tooa.</span><span class="sxs-lookup"><span data-stu-id="5c030-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="5c030-123">Antes de executar o script de Olá, atribua o grupo de recursos toohello etiquetas necessárias de todos os.</span><span class="sxs-lookup"><span data-stu-id="5c030-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="5c030-124">Cada etiqueta no grupo de recursos de Olá é necessária para os recursos de Olá no grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c030-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="5c030-125">grupos de recursos de tooall tooassign na sua subscrição, não fornecem Olá `-Name` parâmetro ao obter grupos de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="5c030-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="5c030-126">Depois de atribuir políticas de Olá, pode acionar um tooall de atualização existente recursos tooenforce Olá tag as políticas que adicionou.</span><span class="sxs-lookup"><span data-stu-id="5c030-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="5c030-127">Olá seguinte script mantém outras etiquetas que existiam recursos Olá:</span><span class="sxs-lookup"><span data-stu-id="5c030-127">hello following script retains any other tags that existed on hello resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="5c030-128">Exigir etiquetas para um tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="5c030-128">Require tags for a resource type</span></span>
<span data-ttu-id="5c030-129">Olá seguinte exemplo mostra como toonest operadores lógicos toorequire uma aplicação tag para apenas um tipo de recurso especificado (neste caso, contas de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="5c030-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="5c030-130">Exigir etiqueta</span><span class="sxs-lookup"><span data-stu-id="5c030-130">Require tag</span></span>
<span data-ttu-id="5c030-131">Olá política seguinte nega pedidos que não tenham uma etiqueta que contém a chave "costCenter" (pode ser aplicada a qualquer valor):</span><span class="sxs-lookup"><span data-stu-id="5c030-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="5c030-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5c030-132">Next steps</span></span>
* <span data-ttu-id="5c030-133">Depois de definir uma regra de política (conforme ilustrado no Olá precedente exemplos), tem de definição de política de Olá toocreate e atribua-lhe tooa âmbito.</span><span class="sxs-lookup"><span data-stu-id="5c030-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="5c030-134">âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="5c030-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="5c030-135">políticas de tooassign através do portal Olá, consulte [tooassign portal do Azure de utilização e gerir políticas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c030-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="5c030-136">políticas de tooassign através da REST API, PowerShell ou o CLI do Azure, consulte [atribuir e gerir políticas através do script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="5c030-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="5c030-137">Para políticas de tooresource uma introdução, consulte [descrição geral da política de recurso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5c030-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="5c030-138">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="5c030-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

